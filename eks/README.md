# EKS - Elastic Kubernetes Service

# Kubernetes as a service offering from Amazon 

## How to connect to AWS account using terminal or cmd

**Dependency** AWS cli needs to be there installed on your local system (mac or windows)

* Also, access key set up done for your root account. Under your account on right hand side just below your account name you will find security credentials. That option can be used to create access key.

Once done with these changes, execute below command which will ask for access key ID and access secret key

    aws configure

Now create iam user, first try to find all applicable options using help 

        aws iam help
        aws iam list-users
        aws iam list-groups
        aws iam create-group --group-name eks-managed-grp
        aws iam create-user --user-name eks-cluster-admin
                *output:
                {
                "User": {
                    "Path": "/",
                    "UserName": "eks-cluster-admin",
                    "UserId": "AIDASVVPYX4GITP7OG2DR",
                    "Arn": "arn:aws:iam::183978475276:user/eks-cluster-admin",
                    "CreateDate": "2022-04-06T14:54:42+00:00"
                }
            }
