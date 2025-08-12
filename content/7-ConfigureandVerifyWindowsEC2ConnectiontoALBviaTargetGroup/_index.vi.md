---
title : "Tạo và cấu hình Target Group cho Windows EC2 với ALB"
date: 2025-08-07
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
## Mục tiêu
Cấu hình Windows EC2 để có thể nhận và phản hồi yêu cầu HTTP từ Application Load Balancer (ALB) thông qua Target Group, đảm bảo health check của Target Group trả về trạng thái Healthy.

## Tạo Target Group

Vào EC2 Console → Target Groups → Create target group.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/1.png) 

Target type: IP.

Protocol: HTTP, Port: 80.

VPC: Select the same VPC as your Linux EC2.

Health check protocol: HTTP.

Health check path: /.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/2.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/3.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/4.png) 

Bấm Next, chọn Private IP của Linux EC2 → Include as pending below → Create target group.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/5.png) 

AWS sẽ yêu cầu bạn Register targets (đăng ký các EC2 vào TG).

Với Linux TG → chọn Private IP của Linux EC2 rồi bấm Include as pending below, sau đó Create target group.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/24.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/25.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/26.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/27.png) 

## Windows Target Group (tương tự Linux nhưng có thay đổi)

Port:

- Linux: 80

- Windows: 8080 (vì IIS/Web app chạy trên 8080).

Health check path:

- Linux: /

- Windows: /win/ (vì trang test đặt trong thư mục win).

Private IP:

- Linux: Private IP của EC2 Linux.

- Windows: Private IP của EC2 Windows.

Security Group rule:

- Linux: Mở cổng 80 cho ALB SG.

- Windows: Mở cổng 8080 cho ALB SG và mở cổng 8080 trong Tường lửa Windows.

Listener / Rule trong ALB:

- Linux: listener HTTP:80 → forward linux-tg (mặc định).

- Windows: thêm quy tắc Path: /win/* → forward windows-tg.

AWS sẽ yêu cầu bạn Đăng ký mục tiêu (đăng ký EC2 với TG).

Với Windows TG → thực hiện tương tự, ngoại trừ Cổng là 8080 và đường dẫn kiểm tra tình trạng là /win/.

## Tạo Application Load Balancer
Vào EC2 Console → Load Balancers → Create Load Balancer → Application Load Balancer.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/11.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/12.png) 

Tên: app-alb.

Scheme: Internet-facing.

IP address type: IPv4.

VPC: trùng với EC2 instances.

Mappings: Chọn ít nhất 2 subnet ở 2 AZ khác nhau.

Security group: Cho phép HTTP (80) từ Anywhere.

Listeners: HTTP trên port 80, forward mặc định tới linux-tg.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/13.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/14.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/15.png) 

Bấm Create load balancer.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/16.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/17.png) 

## Thêm Listener Rule

Chọn ALB app-alb → Listeners → HTTP:80 → View/edit rules

Thêm Rule:

IF Path is /win/* → Forward to windows-tg

Giữ default rule forward tới linux-tg

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/18.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/19.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/20.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/21.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/22.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/23.png) 

## Cấu hình IIS trên Windows Instance

(Nếu chưa cài IIS và binding 8080, chạy các lệnh này trong PowerShell – Run as Administrator)

dism /online /enable-feature /featurename:IIS-WebServerRole /all
dism /online /enable-feature /featurename:IIS-ManagementConsole

New-Item -ItemType Directory -Path "C:\inetpub\wwwroot\win" -Force | Out-Null
"Hello from Windows $env:COMPUTERNAME" | Out-File "C:\inetpub\wwwroot\win\index.html" -Encoding utf8

Import-Module WebAdministration
New-WebBinding -Name "Default Web Site" -Protocol http -Port 8080 -IPAddress "*"

New-NetFirewallRule -DisplayName "IIS 8080 Inbound" -Direction Inbound -Protocol TCP -LocalPort 8080 -Action Allow

iisreset

Truy cập http://localhost:8080/win/ trong Windows instance sẽ hiển thị Hello from Windows…

## Kiểm tra Health Check

Vào Target Groups → linux-tg & windows-tg

Đảm bảo trạng thái cả hai là healthy

Truy cập qua ALB DNS để xác nhận routing hoạt động.
