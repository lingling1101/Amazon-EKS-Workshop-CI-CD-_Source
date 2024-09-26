---
title : "Amazon EKS Workshop - CI/CD với CodePipeline"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Amazon EKS Workshop - CI/CD với CodePipeline

### Tổng quan

Trong bài lab này, chúng ta sẽ tiến hành tạo một CI/CD pipeline sử dụng AWS CodePipeline. CI/CD pipeline sẽ triển khai một dịch vụ mẫu trên EKS cluster của bạn. Sau đó chúng ta sẽ cập nhật thay đổi trên GitHub repository và theo dõi việc triển khai tự động thay đổi này lên trên EKS cluster.

### Nội dung

 1. [Tạo IAM Role](./1-Create/)
 2. [Chỉnh sửa aws-auth](./2-Edit/)
 3. [Fork Repository](./3-Fork/)
 4. [Tạo GitHub access token](./4-CreateGit/)
 5. [Cài đặt CodePipeline](./5-CodePipeline/)
 6. [Kích hoạt New Release](./6-NewRelease/)
 7. [Dọn dẹp tài nguyên](./7-Clean/)
