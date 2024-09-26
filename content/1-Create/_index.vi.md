---
title : "Tạo IAM Role"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
## **1. Tạo IAM Role**

Trong AWS CodePipeline, chúng ta sẽ sử dụng AWS CodeBuild để triển khai một dịch vụ Kubernetes mẫu.Việc này sẽ yêu cầu chúng ta tạo một IAM Role để làm việc với EKS cluster. Trong bước này , chúng ta sẽ tạo 1 IAM Role và gán 1 inline policy ( policy gán trực tiếp ) vào role, việc này cho phép chúng ta sử dụng CodeBuild để tương tác với EKS cluster thông qua **kubectl**.

## **1.1. Chạy câu lệnh dưới đây trong CloudShell**

```bash
mkdir environment

cd ~/environment

TRUST="{ \"Version\": \"2012-10-17\", \"Statement\": [ { \"Effect\": \"Allow\", \"Principal\": { \"AWS\": \"arn:aws:iam::${ACCOUNT_ID}:root\" }, \"Action\": \"sts:AssumeRole\" } ] }"

echo '{ "Version": "2012-10-17", "Statement": [ { "Effect": "Allow", "Action": "eks:Describe*", "Resource": "*" } ] }' > /tmp/iam-role-policy

aws iam create-role --role-name EksWorkshopCodeBuildKubectlRole --assume-role-policy-document "$TRUST" --output text --query 'Role.Arn'

aws iam put-role-policy --role-name EksWorkshopCodeBuildKubectlRole --policy-name eks-describe --policy-document file:///tmp/iam-role-policy
```

![image.png](/images/1.CreateIAM/1-1.png)

## **1.2. Câu lệnh trên giúp chúng ta tạo một IAM Role có tên EksWorkshopCodeBuildKubectlRole và được cấp quyền theo policy dưới đây.**

![image.png](/images/1.CreateIAM/1-2.png)