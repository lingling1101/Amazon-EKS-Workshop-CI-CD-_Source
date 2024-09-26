---
title : "Trigger New Release"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

## **6. Trigger New Release**

In this step, we will edit the **main.go** file to change the greeting to **Welcome to CI/CD Pipeline lab**. Then, we will monitor the release process and check the results.

## **6.1. Access the GitHub Repository you forked in Step 3.**

- Click on the **main.go** file.
  
![image.png](/images/6.NewRelease/6-1.png)

## **6.2. Click on the edit icon.**

![image.png](/images/6.NewRelease/6-2.png)

## **6.3. Change the greeting on line 18 from** Hello World **to** Welcome to CI/CD Pipeline lab.

![image.png](/images/6.NewRelease/6-3.png)

## **6.4. Scroll down to the bottom.**

- Click **Commit changes** to update the code changes.
  
## **6.5. Access the** CodePipeline **service.**

- Click on the **eksws-codepipeline…**.
- Check that the Pipeline has been triggered.

![image.png](/images/6.NewRelease/6-4.png)

## **6.6. Once the build step is complete, go back to the browser where the sample service is running and refresh the page. You should see that the greeting message has been updated.**

![image.png](/images/6.NewRelease/6-5.png)

Congratulations on completing the CI/CD lab with CodePipeline.