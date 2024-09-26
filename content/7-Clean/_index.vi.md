---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---

Chúng ta sẽ tiến hành các bước sau để xóa các tài nguyên chúng ta đã tạo trong bài thực hành này.

## **7. Dọn dẹp tài nguyên**
- Dừng proxy và xóa deployment và service.

```jsx
kubectl delete deployments hello-k8s

kubectl delete services hello-k8s

```

- Truy cập vào giao diện dịch vụ CloudFormation.
    - Click chọn **eksws-codepipeline**.
    - Click **Delete**.

- Truy cập vào giao diện dịch vụ Elastic Container Registry.
    - Click chọn **eksws-codepipeline…**.
    - Click **Delete**.

- Truy cập vào giao diện dịch vụ S3.

Click chọn bucket **eksws-codepipeline… →** Click **Empty**.

Tại trang **Delete bucket**.