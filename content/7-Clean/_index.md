---
title : "Clean up resources"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---

We will perform the following steps to delete the resources we created during this lab.

## **7. Clean up resources**
   
- Stop the proxy and delete the deployment and service.

```jsx
kubectl delete deployments hello-k8s

kubectl delete services hello-k8s

```

- Access the CloudFormation service interface.
    - Click on **eksws-codepipeline**.
    - Click **Delete**.

- Access the Elastic Container Registry service interface.
    - Click on **eksws-codepipeline…**.
    - Click **Delete**.

- Access the S3 service interface.

Click on the bucket **eksws-codepipeline… →** Click **Empty**.

On the **Delete bucket** page.