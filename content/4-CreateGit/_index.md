---
title : "Create GitHub access token"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
## **4. Create GitHub access token**

To allow CodePipeline to receive callbacks from GitHub, we need to create a personal access token. Once created, the access token will be stored and reused, so this step only needs to be done once.

## **4.1. Open the [Personal access token](https://github.com/settings/tokens/new) management page on GitHub.**

- In the **Note** field, enter **eks-workshop**.
- Select **repo**.

![image.png](/images/4.Git/4-1.png)

## **4.2. Scroll down to the bottom and click** Generate token

![image.png](/images/4.Git/4-2.png)

## **4.3. Click the copy icon to save the access token for use in the following steps.**

![image.png](/images/4.Git/4-3.png)


