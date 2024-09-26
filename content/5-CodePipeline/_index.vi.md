---
title : "Cài đặt CodePipeline"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
## **5. Cài đặt CodePipeline**

Trong bước này chúng ta sẽ cài đặt CodePipeline sử dụng AWS CloudFormation,

CloudFormation là một công cụ Infrastructure as code (IaC) cung cấp một ngôn ngữ chung để mô tả và khởi tạo các tài nguyên hạ tầng trong môi trường điện toán đam mây. CloudFormation cho phép chúng ta sử dụng một cấu trúc text-base đơn giản để mô tả và khởi tạo tài nguyên trong môi trường tự động hóa một cách bảo mật, hỗ trợ tất cả các tài nguyên mà ứng dụng cần trên tất cả các AWS Regions và AWS Accounts. Mỗi một dịch vụ EKS được triển khai sẽ có CodePipeline riêng cùng với source repository độc lập.

## **5.1. Tải về file CloudFormation template dưới đây.**

[https://000152.awsstudygroup.com/5-setup-codepipeline/_index.files/ci-cd-codepipeline.cfn.yml](https://000152.awsstudygroup.com/5-setup-codepipeline/_index.files/ci-cd-codepipeline.cfn.yml)

## **5.2. Truy cập vào dịch vụ CloudFormation** [https://console.aws.amazon.com/cloudformation/](https://console.aws.amazon.com/cloudformation/)

- Click **Create stack**.
- Click **With new resources(standard)**.

![image.png](/images/5.CodePipeline/5-1.png)

## **5.3. Tại trang** Create stack.

- Click **Template is ready**.
- Click **Upload a template file**.
- Chọn file đã download về có tên **ci-cd.codepipeline.cfn.yml**.
- Click **Next**.

![image.png](/images/5.CodePipeline/5-2.png)

## **5.4. Tại trang** Specify stack details.

- Điền Stack name : **eksws-codepipeline**.
- Điền Git Hub Username : <Username GitHub của bạn>.
- Điền GitHub Acess token: <Personal access token bạn tạo ở bước 4>.

![image.png](/images/5.CodePipeline/5-3.png)

## **5.5. Kéo màn hình xuống dưới và click** Next.**

## **5.6.Tại trang** Configure stack Options, **kéo màn hình xuống dưới và click** Next.

## **5.7. Tại trang** Review eksws-codepipeline, **kéo màn hình xuống dưới.**

- Click chọn **I acknowledge that AWS CloudFormation might create IAM resources.**
- Click **Create stack**.

## **5.8. Kiểm tra trạng thái tạo stack** eksws-codepipeline **thành công như hình.**

![image.png](/images/5.CodePipeline/5-4.png)

## **5.9. Truy cập trang dịch vụ** CodePipeline, **chúng ta sẽ thấy trạng thái tạo CodePipeline thành công**.

- Click vào tên của **eksws-codepipeline….**

![image.png](/images/5.CodePipeline/5-5.png)

## **5.10. Kiểm tra trạng thái build thành công:**

- Click vào **Details**.

## **5.11. Bạn có thể xem được logs của toàn bộ quá trình build**

![image.png](/images/5.CodePipeline/5-6.png)

**Kiểm tra dịch vụ mẫu**

- Chạy câu lệnh dưới đây để kiểm tra trạng thái triển khai của dịch vụ mẫu.

```jsx
kubectl describe deployment hello-k8s
```

![image.png](/images/5.CodePipeline/5-7.png)

- Chạy câu lệnh dưới đây để kiểm tra trạng thái của dịch vụ.

```jsx
kubectl describe service hello-k8s
```

![image.png](/images/5.CodePipeline/5-8.png)

- Chạy câu lệnh dưới đây để lấy thông tin Elastic Load Balancer (ELB) endpoint và lưu thông tin **EXTERNAL-IP** lại.

```jsx
kubectl get services hello-k8s -o wide
```

- Truy cập trên một tab trình duyệt mới. Chúng ta sẽ thấy dịch vụ mẫu gửi lời chào **Hello World** và cung cấp các thông tin của EKS cluster.

Ở bước tiếp theo chúng ta sẽ thay đổi nội dung lời chào trên GitHub repository và kiểm tra hoạt động của Pipeline. ![image.png](/images/5.CodePipeline/5-9.png)
