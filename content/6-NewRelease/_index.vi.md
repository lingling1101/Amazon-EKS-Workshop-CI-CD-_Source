---
title : "Kích hoạt New Release"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
## **6. Kích hoạt New Release**

Trong bước này chúng ta sẽ chỉnh sửa file **main.go** để thay đổi lời chào thành **Welcome to CI/CD Pipeline lab**. Sau đó theo dõi quá trình release và kiểm tra kết quả.

## **6.1. Truy cập vào GitHub Repository bạn đã fork ở bước 3.**

- Click vào file **main.go**.

![image.png](/images/6.NewRelease/6-1.png)

## **6.2. Click vào biểu tượng chỉnh sửa.**

![image.png](/images/6.NewRelease/6-2.png)

## **6.3. Thay đổi nội dung lời chào ở dòng số 18 từ** Hello World **thành** Welcome to CI/CD Pipeline lab.

![image.png](/images/6.NewRelease/6-3.png)

## **6.4. Kéo màn hình xuống dưới cùng.**

- Click **Commit changes** để cập nhật thay đổi code.

## **6.5. Truy cập vào dịch vụ** CodePipeline**.**

- Click vào pipeline **eksws-codepipeline…**.
- Kiểm tra Pipeline đã được kích hoạt.

![image.png](/images/6.NewRelease/6-4.png)

## **6.6. Sau khi bước build hoàn tất, quay lại trình duyệt đang truy cập vào dịch vụ mẫu và thực hiện refresh, bạn sẽ thấy thông tin lời chào đã được update.**

![image.png](/images/6.NewRelease/6-5.png)

Chúc mừng bạn đã hoàn thành bài lab xây dựng CI/CD với CodePipeline.