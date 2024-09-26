---
title : "Set up CodePipeline"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
## **5. Set up CodePipeline**

In this step, we will set up CodePipeline using AWS CloudFormation.

CloudFormation is an Infrastructure as Code (IaC) tool that provides a common language to describe and provision infrastructure resources in a cloud computing environment. CloudFormation allows us to use a simple text-based structure to describe and provision resources in an automated and secure manner, supporting all the resources needed by the application across all AWS Regions and AWS Accounts. Each EKS service deployed will have its own CodePipeline along with an independent source repository.

## **5.1. Download the CloudFormation template file below.**

[https://000152.awsstudygroup.com/5-setup-codepipeline/_index.files/ci-cd-codepipeline.cfn.yml](https://000152.awsstudygroup.com/5-setup-codepipeline/_index.files/ci-cd-codepipeline.cfn.yml)

## **5.2. Access the CloudFormation service** [https://console.aws.amazon.com/cloudformation/](https://console.aws.amazon.com/cloudformation/)

- Click **Create stack**.
- Click **With new resources (standard)**.

![image.png](/images/5.CodePipeline/5-1.png)

## **5.3. On the** Create stack **page**.

- Click **Template is ready**.
- Click **Upload a template file**.
- Select the downloaded file named **ci-cd.codepipeline.cfn.yml**.
- Click **Next**.

![image.png](/images/5.CodePipeline/5-2.png)

## **5.4. On the** Specify stack details **page**.

- Enter Stack name: **eksws-codepipeline**.
- Enter GitHub Username: <Your GitHub Username>.
- Enter GitHub Access token: <The personal access token you created in Step 4>.

![image.png](/images/5.CodePipeline/5-3.png)

## **5.5. Scroll down and click** Next.

## **5.6. On the** Configure stack options **page, scroll down and click** Next.

## **5.7. On the** Review eksws-codepipeline **page, scroll down.**

- Check **I acknowledge that AWS CloudFormation might create IAM resources.**
- Click **Create stack**.

## **5.8. Verify that the stack creation status for** eksws-codepipeline **is successful, as shown below.**

![image.png](/images/5.CodePipeline/5-4.png)

## **5.9. Access the CodePipeline service page, and you will see the successful creation status of CodePipeline.**

- Click on the name **eksws-codepipeline….**

![image.png](/images/5.CodePipeline/5-5.png)

## **5.10. Verify that the build status is successful:**

- Click on **Details**.

## **5.11. You can view the logs of the entire build process.**

![image.png](/images/5.CodePipeline/5-6.png)

**Check the sample service**

- Run the following command to check the deployment status of the sample service.

```jsx
kubectl describe deployment hello-k8s
```

![image.png](/images/5.CodePipeline/5-7.png)

- Run the following command to check the status of the service.

```jsx
kubectl describe service hello-k8s
```

![image.png](/images/5.CodePipeline/5-8.png)

- Run the following command to retrieve the Elastic Load Balancer (ELB) endpoint information and note down the **EXTERNAL-IP**.

```jsx
kubectl get services hello-k8s -o wide
```

- Access it in a new browser tab. You should see the sample service greeting **Hello World** and displaying the details of the EKS cluster.

In the next step, we will modify the greeting message in the GitHub repository and test the Pipeline's operation. ![image.png](/images/5.CodePipeline/5-9.png)
