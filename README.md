# kubernetes
This repository has all the details and understanding required for Kubernetes and EKS - ECS

# Define an admin user with privilege to create / delete / manage EKS cluster

Login to management console and create a user with programtic access 

IAM -- > Users -- > Add Users -- > Provide name and select programmatic access (this is because we dont need console access) -- > Permission (Attach existing policy directly) -- > create policy -- > in the service tab select EKS -- > under actions select all -- > in resources tab select all resource -- > leave request condition -- > finally review and provide name to the policy (something like EKS_cluster_admin_policy) -- > come back to user creation tab -- > refresh policy list -- > search for your policy (EKS_cluster_admin_policy) and select -- > go for next -- > finally create user

Also map one more policy to the user 

IAM -- > Users -- > click on your user -- > Permission -- > Add permission -- > Attach existing policy directly -- > search for admin -- > select administratoraccess -- > review and add permission


# lets create cluster without nodegroup initially 

eksctl create cluster --name raining-demo-01 --region=ap-south-1 --zones=ap-south-1a,ap-south-1b --without-nodegroup

