# kubernetes
This repository has all the details and understanding required for Kubernetes and EKS - ECS

# Define an admin user with privilege to create / delete / manage EKS cluster

Login to management console and create a user with programtic access <br/>

IAM -- > Users -- > Add Users -- > Provide name and select programmatic access (this is because we dont need console access) -- > Permission (Attach existing policy directly) -- > create policy -- > in the service tab select EKS -- > under actions select all -- > in resources tab select all resource -- > leave request condition -- > finally review and provide name to the policy (something like EKS_cluster_admin_policy) -- > come back to user creation tab -- > refresh policy list -- > search for your policy (EKS_cluster_admin_policy) and select -- > go for next -- > finally create user

Also map one more policy to the user </br>

IAM -- > Users -- > click on your user -- > Permission -- > Add permission -- > Attach existing policy directly -- > search for admin -- > select administratoraccess -- > review and add permission


# lets create cluster without nodegroup initially 

eksctl create cluster --name raining-demo-01 --region=ap-south-1 --zones=ap-south-1a,ap-south-1b --without-nodegroup

# Now map associate-iam-oidc-provider to the cluster you have created 

eksctl utils associate-iam-oidc-provider --region=ap-south-1 --cluster=raining-demo-01 --approve

# Now we are all set to create nodegroup 

# But before that login to AWS console and create keypair which we will be using to map EC2 node (only if you want to access it remotely)

eksctl create nodegroup --name=raining-demo-01-ng-01 \
--node-type=t2.small \
--nodes=2 \
--nodes-min=2 \
--nodes-max=3 \
--node-volume-size=20 \
--ssh-access \
--managed \
--asg-access  \
--external-dns-access \
--full-ecr-access \
--alb-ingress-access  \
--appmesh-access  \
--cluster=raining-demo-01 \
--region=ap-south-1 \
--ssh-public-key=generic  \
--node-labels=k1=v1,k2=v2,k3=v3

# Delete a nodegroup

eksctl get nodegroup --cluster=raining-demo-01 --region=ap-south-1
eksctl delete nodegroup raining-demo-01-ng-01 --cluster=raining-demo-01 --region=ap-south-1

# Delete a cluster

eksctl delete cluster --name=raining-demo-01

# By default Kubernetes object will not be accessible to anyone, we need to define RBAC role association with the user in order to access kubernetes objecrs

Make a file - user.yml and execute command eksctl create -f user.yml (Here eks-user-cluster-read-write is the name of user, for which we are defining authorization) 

apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: developer-clusterrole
rules:
  - apiGroups: [""]
    resources: ["nodes", "namespaces", "pods"]
    verbs: ["get", "list"]
  - apiGroups: ["apps"]
    resources: ["deployments" ,"daemonsets" ,"statefulsets" ,"replicasets"]
    verbs: ["get", "list", "create"]
  - apiGroups: [ "batch"]
    resources: ["jobs"]
    verbs: ["get", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: developer-clusterrole-binding
subjects:
  - kind: User
    name: eks-user-cluster-read-write
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: developer-clusterrole
  apiGroup: rbac.authorization.k8s.io
  
  kind: ClusterRole is for cluster and kind: Role is for namespace


# RBAC - Role Based Access Control within kubernetes cluster to manage cluster objects. 

You may need to have different role associated with users and groups, in order to manage different k8s objects and cluster itself.

In k8s we have role and that can be mapped to users and groups using RoleBinding. Role and RoleBinding lives at namespace level. 




