---
title : "Tạo GitHub access token"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
## **4. Tạo GitHub access token**

Để cho CodePipeline có thể nhận callbacks từ GitHub, chúng ta sẽ cần tạo ra một personal access token. Sau khi tạo ra , access token sẽ được lưu trữ và tái sử dụng, bước này chúng ta chỉ cần làm một lần.

## **4.1. Mở trang quản lý [Personal access token](https://github.com/settings/tokens/new) của GitHub.**

- Tại mục **Note** điền tên **eks-workshop**.
- Click chọn **repo**.

![image.png](/images/4.Git/4-1.png)

## **4.2. Kéo màn hình xuống dưới cùng, click** Generate token

![image.png](/images/4.Git/4-2.png)

## **4.3. Click vào biểu tượng copy để lưu thông tin access token, phục vụ cho các bước tiếp theo**

![image.png](/images/4.Git/4-3.png)


