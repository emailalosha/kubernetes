# kubernetes
This repository has all the details and understanding required for Kubernetes and EKS - ECS

# Define an admin user with privilege to create / delete / manage EKS cluster

Login to management console and create a user with programtic access 

IAM -- > Users -- > Add Users -- > Provide name and select programmatic access (this is because we dont need console access) -- > Permission (Attach existing policy directly) -- > create policy -- > in the service tab select EKS -- > under actions select all -- > in resources tab select all resource -- > leave request condition -- > finally review and provide name to the policy (something like EKS_cluster_admin_policy) -- > come back to user creation tab -- > refresh policy list -- > search for your policy (EKS_cluster_admin_policy) and select -- > go for next -- > finally create user

Also map one more policy to the user 

IAM -- > Users -- > click on your user -- > Permission -- > Add permission -- > Attach existing policy directly -- > search for admin -- > select administratoraccess -- > review and add permission


# lets create cluster without nodegroup initially 

eksctl create cluster --name raining-demo-01 --region=ap-south-1 --zones=ap-south-1a,ap-south-1b --without-nodegroup

# Now map associate-oidc-iam-provider to the cluster you have created 

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


