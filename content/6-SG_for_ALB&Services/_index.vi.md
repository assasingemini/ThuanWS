---
title : "Tạo Security Groups (SG) cho ALB & Services"
date: 2025-08-07
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
## Mục tiêu
ALB nhận HTTP từ Internet.

Chỉ ALB mới có thể truy cập các container Linux (cổng 5000) và container Windows (cổng 8080).

Theo mặc định, Outbound được đặt thành Allow all.

## SG cho ALB (alb-sg)
Vào EC2 → Security Groups → Create security group.

![SG](images/6-SG_for_ALB&Services/2.png) 

Security group name: alb-sg

Description: ALB allow HTTP 80 from Internet

VPC: VPC đang hoạt động của bạn.

Inbound rules → Add rule

Type: HTTP

Port range: 80

Source: 0.0.0.0/0 (optionally ::/0 if using IPv6)

Outbound rules: giữ nguyên mặc định All traffic (0.0.0.0/0).

![SG](images/6-SG_for_ALB&Services/3.png) 

Sau đó, nhấp vào "Create security group".

## SG cho dịch vụ Linux (ecs-linux-sg)
Vào EC2 → Security Groups → Create security group.

Security group name: ecs-linux-sg

Description: Allow ALB to Linux service on port 5000

VPC: cùng VPC với ALB.

Inbound rules → Add rule

Type: Custom TCP

Port range: 5000

Source: Custom → Security group, sau đó select alb-sg (search by sg-... or name).

Quan trọng: nguồn phải là SG alb-sg, không phải 0.0.0.0/0.

Outbound rules: giữ nguyên mặc định là All traffic.

![SG](images/6-SG_for_ALB&Services/4.png) 

Tags → Add tag: Name = ecs-linux-sg. Sau đó, bấm vào "Create security group".

![SG](images/6-SG_for_ALB&Services/5.png) 

## SG cho dịch vụ Windows (ecs-win-sg)
Tương tự như tạo ecs-linux-sg cho Linux, chỉ cần một số thay đổi

![SG](images/6-SG_for_ALB&Services/6.png) 

Dưới đây là kết quả chúng ta nhận được sau khi tạo SecurityGroups

![SG](images/6-SG_for_ALB&Services/7.png) 