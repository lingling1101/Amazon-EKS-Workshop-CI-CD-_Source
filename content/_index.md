---
title : "Amazon EKS Workshop - CI/CD với CodePipeline"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
### Overview

In this lab, we will create a CI/CD pipeline using AWS CodePipeline. The CI/CD pipeline will deploy a sample service on your EKS cluster. Afterward, we will update the changes in a GitHub repository and monitor the automatic deployment of these changes to the EKS cluster.

### Nội dung

 1. [Create IAM Role](./1-Create/)
 2. [Edit aws-auth](./2-Edit/)
 3. [Fork Repository](./3-Fork/)
 4. [Create GitHub access token](./4-CreateGit/)
 5. [Set up CodePipeline](./5-CodePipeline/)
 6. [Trigger New Release](./6-NewRelease/)
 7. [Clean up resources](./7-Clean/)
