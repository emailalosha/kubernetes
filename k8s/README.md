                                                                                  # K8s
 

# Minikube is a single node Kubernetes cluster where you can hands on fundamental kubernetes. 

 -- Once you are done with installation and configuration on minikube 
 
minikube start --vm-driver=hyperkit



Namespaces

Namespaces are intended for use in environments with many users spread across multiple teams, or projects. For clusters with a few to tens of users, you should not need to create or think about namespaces at all. Start using namespaces when you need the features they provide.
Namespaces provide a scope for names. Names of resources need to be unique within a namespace, but not across namespaces. Namespaces cannot be nested inside one another and each Kubernetes resource can only be in one namespace.
Namespaces are a way to divide cluster resources between multiple users (via resource quota).
It is not necessary to use multiple namespaces to separate slightly different resources, such as different versions of the same software: use labels to distinguish resources within the same namespace.

Get all namaspaces

kubectl get namespace/ns

Create a namespace 
kubectl create namespace namespace_name/raining-lab

Setting namespace preference 
kubectl config set-context --current --namespace=namespace_name
kubectl config set-context --current --namespace=raining-lab


Pod is the smallest unit of the Kubernetes cluster. You can say it is a wrapper around a container. Within a pod it is recommended to have only one container. Sometimes in exceptional scenarios we may have more than one container within a pod, and that too with one of the containers acting as helper for the main container. Helper refers to push or pull of data used by the main container etc. 

You can create pod independently using declarative approach of yaml file. 

API version ref. 

https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#pod-v1-core


apiVersion: v1
kind: Pod
metadata:
 name: raining-lab-pod-1
 labels:
   app: raining-lab-pod-1
spec:
 containers:
   - name: raining-lab-pod-1
     image: nginx:latest
     ports:
       - containerPort: 80


# apiVersion you need to refer to kubernetes doc. 
# kind refers to the kind of kubernetes object you wanted to manage. 
# metadata will have meta information (name, label etc.) about the kubernetes object. 

# These three - apiVersion, kind and metadata makes skelton of kuberenetes object's yaml declerartion

spec is where we need to define what exactly we are trying to manage using this kubernetes object. E.g. For Pod objects we need to define containers within spec. And containers needs details like name, image, ports etc. 

# Pod has a limitation, where assigned IP is getting changed with each restart. And hence we need some sort of other object on top of POD which can connect with it internally and expose connectivity to the external world. This can be done using service or Node service. 

Aloks-MacBook-Pro:kubernetes alokk$ kubectl get po -o wide
NAME                READY   STATUS    RESTARTS   AGE    IP           NODE       NOMINATED NODE   READINESS GATES
raining-lab-pod-1   1/1     Running   0          2m4s   172.17.0.5   minikube   <none>           <none>



Also by using Pod we can define a single pod, however to create replicas we can make use of replicaSet. 

kubectl create -f pod-definition.yml 
Above command is going to create and run the pod. 

Steps going to execute at pod level (high level)

kubectl describe pod pod_name/pod_id

Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  3m15s  default-scheduler  Successfully assigned raining-lab/raining-lab-rs-1-6ft5x to minikube
  Normal  Pulling    3m14s  kubelet            Pulling image "nginx:latest"
  Normal  Pulled     3m7s   kubelet            Successfully pulled image "nginx:latest" in 7.358869091s
  Normal  Created    3m7s   kubelet            Created container raining-lab-pod-sample-con
  Normal  Started    3m7s   kubelet            Started container raining-lab-pod-sample-con



ReplicaSet will also have the same skeleton as in Pod with very little difference. 

apiVersion: apps/v1
kind: ReplicaSet
metadata:
 name: raining-lab-rs-1
 labels:
   app: raining-lab-rs-1
spec:
 replicas: 2
 selector:
   matchLabels:
     app: raining-lab-pod-sample
 template:
   metadata:
     name: raining-lab-pod-sample
     labels:
       app:  raining-lab-pod-sample
   spec:
     containers:
       - name: raining-lab-pod-sample-con
         image: nginx:latest
         ports:
           - containerPort: 80


# Within spec: matchLabels reference to label of Pod and replicas is number of replica pods we wanted to create within kubernetes cluster. And the template is Pod information. 

kubectl create -f replicaset-definition.yml

Above command is going to create replicaset, and associated Pod within kubernetes cluster. 

kubectl get rs
kubectl get rs -o wide

apiVersion: v1
kind: Service
metadata:
 name: raining-lab-service
 labels:
   app: raining-lab-service
spec:
 type: NodePort
 selector:
   app: raining-lab-pod-sample
 ports:
     - name: http
       nodePort: 30283
       port: 80
       targetPort: 80


Storage is not provided by Kubernetes by default. You have the option to configure it. 

Storage doesn’t depend on the pod lifecycle. 
Storage must be available for all nodes. 
Storage needs to survive even after pod crash 

Persistent Volume 
Persistent Volume Claim 






Secrets 

Secrets are those sensitive data on which our pod or container depends. Or you can say these are those environment variables which are needed by your container to run or start. It is always recommended to keep sensitive data out of the pod and also needs to be either encoded or encrypted. 

apiVersion: v1
kind: Secret
metadata:
 name: my-sql-db-password
type: Opaque
data:
 db-password: cGFzc3dvcmQ= # base64 encoded value
 db-username: YWRtaW4=
 db-host: bG9jYWxob3N0

Above is a secret-difinition.yml file containing data like db_password, db_username etc. lets create a secret object first. 

– value of the key needs to be encoded atleast for sure. 

kubetctl apply -f secret-definition.yml

Now we can use keys of secret directly within any other kubernetes object. 

apiVersion: apps/v1
kind: Deployment
metadata:
 name: raining-lab-deployment-1
 labels:
   app: raining-lab-app1
spec:
 replicas: 2
 selector:
   matchLabels:
     app: raining-lab-app1
 template:
   metadata:
     name: raining-lab-app1
     labels:
       app: raining-lab-app1
   spec:
     containers:
       - name: raining-lab-app1
         image: nginx:latest
         env:
           - name: MY-SQL-DB-PASSWORD
             valueFrom:
               secretKeyRef:
                 name: my-sql-db-password
                 key: db-password
         ports:
           - containerPort: 80

After running above deployment-definition.yml when we will login to container as root and see environment then we can find MY-SQL-DB-PASSWORD as well. 

Namespaces

Namespaces are virtual cluster within main physical cluster. Or you can say it is subset of cluster. 

It provides isolated boundary for kubernetes objects within a cluster. 


kubectl exec --stdin --tty shell-demo -- /bin/bash
