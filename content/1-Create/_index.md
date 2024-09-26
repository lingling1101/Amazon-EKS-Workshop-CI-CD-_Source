---
title : "Create IAM Role"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
## **1. Create IAM Role**

In AWS CodePipeline, we will use AWS CodeBuild to deploy a sample Kubernetes service. This requires us to create an IAM Role to work with the EKS cluster. In this step, we will create an IAM Role and attach an inline policy to the role, which allows us to use CodeBuild to interact with the EKS cluster via **kubectl**.

## **1.1. Run the following command in CloudShell**

```bash
mkdir environment

cd ~/environment

TRUST="{ \"Version\": \"2012-10-17\", \"Statement\": [ { \"Effect\": \"Allow\", \"Principal\": { \"AWS\": \"arn:aws:iam::${ACCOUNT_ID}:root\" }, \"Action\": \"sts:AssumeRole\" } ] }"

echo '{ "Version": "2012-10-17", "Statement": [ { "Effect": "Allow", "Action": "eks:Describe*", "Resource": "*" } ] }' > /tmp/iam-role-policy

aws iam create-role --role-name EksWorkshopCodeBuildKubectlRole --assume-role-policy-document "$TRUST" --output text --query 'Role.Arn'

aws iam put-role-policy --role-name EksWorkshopCodeBuildKubectlRole --policy-name eks-describe --policy-document file:///tmp/iam-role-policy
```

![image.png](/images/1.CreateIAM/1-1.png)

## **1.2. The above command helps us create an IAM Role named EksWorkshopCodeBuildKubectlRole with the permissions defined by the policy below.**

![image.png](/images/1.CreateIAM/1-2.png)