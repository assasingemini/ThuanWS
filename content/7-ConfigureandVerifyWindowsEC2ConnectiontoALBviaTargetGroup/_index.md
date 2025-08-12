---
title : "Create and Configure Windows EC2 Target Group with ALB"
date: 2025-08-07
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
## Objective
Configure Windows EC2 to receive and respond to HTTP requests from an Application Load Balancer (ALB) via a Target Group, ensuring the Target Group health check returns a Healthy status.

## Tạo Target Group

Navigate to EC2 Console → Target Groups → Create target group.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/1.png) 

Target type: IP

Protocol: HTTP, Port: 80

VPC: Select the same VPC as your Linux EC2

Health check protocol: HTTP

Health check path: /

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/2.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/3.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/4.png) 

Click Next, select the Private IP of the Linux EC2 → Include as pending below → Create target group.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/5.png) 

AWS will prompt you to register targets (register EC2s to TG).

With Linux TG → select Private IP of Linux EC2 then click Include as pending below, then Create target group.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/24.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/25.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/26.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/27.png) 

## Windows Target Group (similar to Linux but with changes)

Port:

- Linux: 80

- Windows: 8080 (because IIS/Web app runs on 8080).

Health check path:

- Linux: /

- Windows: /win/ (because the test page is located in the win folder).

Private IP:

- Linux: Private IP of EC2 Linux.

- Windows: Private IP of EC2 Windows.

Security Group rule:

- Linux: Mở port 80 cho ALB SG.

- Windows: Mở port 8080 cho ALB SG và mở port 8080 trong Windows Firewall.

Listener / Rule trong ALB:

- Linux: listener HTTP:80 → forward linux-tg (mặc định).

- Windows: thêm rule Path: /win/* → forward windows-tg.

AWS sẽ yêu cầu bạn Register targets (đăng ký các EC2 vào TG).

Với Windows TG → làm tương tự, chỉ khác Port là 8080 và Health check path là /win/.

## Tạo Application Load Balancer
Vào EC2 Console → Load Balancers → Create Load Balancer → Application Load Balancer.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/11.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/12.png) 

Name: app-alb.

Scheme: Internet-facing.

IP address type: IPv4.

VPC: same as EC2 instances.

Mappings: Select at least 2 subnets in 2 different AZs.

Security group: Allow HTTP (80) from Anywhere.

Listeners: HTTP on port 80, default forward to linux-tg.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/13.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/14.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/15.png) 

Click Create load balancer.

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/16.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/17.png) 

## Add Listener Rule

Select ALB app-alb → Listeners → HTTP:80 → View/edit rules

Add Rules:

IF Path is /win/* → Forward to windows-tg

Keep default rule forward to linux-tg

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/18.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/19.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/20.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/21.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/22.png) 

![tg](images/7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/23.png) 

## Configuring IIS on Windows Instance

(If you don't have IIS installed and binding 8080, run these commands in PowerShell – Run as Administrator)

dism /online /enable-feature /featurename:IIS-WebServerRole /all
dism /online /enable-feature /featurename:IIS-ManagementConsole

New-Item -ItemType Directory -Path "C:\inetpub\wwwroot\win" -Force | Out-Null
"Hello from Windows $env:COMPUTERNAME" | Out-File "C:\inetpub\wwwroot\win\index.html" -Encoding utf8

Import-Module WebAdministration
New-WebBinding -Name "Default Web Site" -Protocol http -Port 8080 -IPAddress "*"

New-NetFirewallRule -DisplayName "IIS 8080 Inbound" -Direction Inbound -Protocol TCP -LocalPort 8080 -Action Allow

iisreset

Accessing http://localhost:8080/win/ in Windows instance will display Hello from Windows…

## Health Check

Go to Target Groups → linux-tg & windows-tg

Ensure both status is healthy

Access via ALB DNS to confirm routing is working.