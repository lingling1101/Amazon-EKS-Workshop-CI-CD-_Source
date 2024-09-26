---
title : "Chỉnh sửa aws-auth"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
## **2. Chỉnh sửa aws-auth**

Sau khi tao IAM Role xong, chúng ta sẽ thêm role đã tạo vào **aws-auth** ConfigMap cho EKS cluster. Sau khi ConfigMap đã được thiết lập cho role mới, kubectl trong CodeBuild stage của pipeline sẽ có thể tương tác với EKS cluster thông qua IAM Role.

## **2.1. Cài đặt** 

**✔️ Cloud9**: Được thiết kế như một IDE trực tuyến, đi kèm với nhiều công cụ phát triển và tiện ích được cài đặt sẵn, bao gồm `kubectl`, `jq`, `aws-cli`, và các gói phát triển khác. Điều này có nghĩa là bạn có thể dễ dàng chạy các lệnh phức tạp mà không gặp phải lỗi thiếu công cụ hoặc thư viện.

**✔️ CloudShell**: Là một terminal dựa trên trình duyệt với một bộ công cụ hạn chế hơn. Một số công cụ phổ biến như `kubectl` có thể không được cài đặt sẵn, và bạn phải tự cài đặt chúng nếu cần.

Các AWS Regions hỗ trợ AWS CloudShell:

- US East (Ohio)
- US East (N. Virginia)
- US West (N. California)
- US West (Oregon)
- Asia Pacific (Mumbai)
- Asia Pacific (Osaka)
- Asia Pacific (Seoul)
- Asia Pacific (Sydney)
- Asia Pacific (Singapore)
- Asia Pacific (Tokyo)
- Canada (Central)
- Europe (Frankfurt)
- Europe (Ireland)
- Europe (London)
- Europe (Paris)
- Europe (Stockholm)
- South America (São Paulo)


 ➖ Cài đặt [kubectl]

```jsx
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

 ➖ Cài đặt [eksctl]) command-line tool

```jsx
# for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH

curl -sLO "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"

# (Optional) Verify checksum
curl -sL "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check

tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz

sudo mv /tmp/eksctl /usr/local/bin
```

Lưu dưới dạng: `eksctl.sh` 

Sau đó:

```jsx
 chmod +x eksctl.sh 
 
 sudo sh eksctl.sh
```

 ➖ Cài đặt EKS Cluster

```jsx
eksctl create cluster --name MY-EKS-CLUSTER --region us-east-1 --nodegroup-name my-nodegroup --node-type t2.small --nodes 3 --nodes-min 1 --nodes-max 5 --managed
```

 ➖ Tạo file `deployment.yaml`

```jsx
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
        
```

 ➖ Triển khai ứng dụng mẫu vào cụm EKS ****

```jsx
kubectl apply -f deployment.yaml
```

 ➖ Hiển thị ứng dụng bằng dịch vụ Kubernetes:

```jsx
kubectl expose deployment nginx-deployment --type=LoadBalancer --name=my-service
```

 ➖ Lấy địa chỉ IP bên ngoài của LoadBalancer:

```jsx
kubectl get services my-service
```

 ➖ Thiết lập HPA, tạo file hpa.yaml

```jsx
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: nginx-deployment-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deployment
  minReplicas: 3
  maxReplicas: 10
  targetCPUUtilizationPercentage: 50
```

 ➖ Áp dụng cấu hình HPA

```jsx
kubectl apply -f hpa.yaml
```

 ➖ Định cấu hình quyền cho tài khoản người dùng IAM

```jsx
kubectl get configmap aws-auth -n kube-system -o yaml > aws-auth.yaml
```

 ➖ Cấu hình quyền cho tài khoản người dùng IAM của bạn

Chỉnh sửa `aws-auth.yaml`

```jsx
apiVersion: v1
data:
  mapRoles: |
    - groups:
      - system:bootstrappers
      - system:nodes
      rolearn: arn:aws:iam::058264096637:role/eksctl-my-eks-cluster-nodegroup-my-NodeInstanceRole-lDyNgcHNtm0l
      username: system:node:{{EC2PrivateDNSName}}
  mapUsers: |
    - userarn: [user-arn-name]
      username: [user-name]
      groups:
        - system:masters

kind: ConfigMap
metadata:
  creationTimestamp: "2024-08-11T09:17:29Z"
  name: aws-auth
  namespace: kube-system
  resourceVersion: "1296"
  uid: 42e53ce2-b732-46a5-bacc-ec6727935b5e
```

Sau đó

```jsx
kubectl apply -f aws-auth.yaml
```

 ➖ Chạy câu lệnh dưới đây trong Cloud

```jsx
ROLE="    - rolearn: arn:aws:iam::**${ACCOUNT_ID}**:role/EksWorkshopCodeBuildKubectlRole\n      username: build\n      groups:\n        - system:masters"

kubectl get -n kube-system configmap/aws-auth -o yaml | awk "/mapRoles: \|/{print;print \"$ROLE\";next}1" > /tmp/aws-auth-patch.yml

kubectl patch configmap/aws-auth -n kube-system --patch "$(cat /tmp/aws-auth-patch.yml)"
```

![image.png](/images/2.Edit/2-1.png)

## **2.2. Kiểm tra lại thông tin AWS auth map với câu lệnh dưới**

```jsx
kubectl describe configmap -n kube-system aws-auth
```

![image.png](/images/2.Edit/2-2.png)

## **2.3. Chúng ta sẽ thấy cấu hình aws-auth được thêm vào cho user build.**

![image.png](/images/2.Edit/2-3.png)





  
