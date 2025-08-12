---
title : "Create Security Groups (SG) for ALB & Services"
date: 2025-08-07
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
## Goal
ALB receives HTTP from the Internet.

Only ALB can access Linux containers (port 5000) and Windows containers (port 8080).

Outbound is set to Allow all by default.

## SG cho ALB (alb-sg)
Go to EC2 → Security Groups → Create security group.

![SG](/ThuanWS/images/6-SG_for_ALB&Services/2.png) 

Security group name: alb-sg

Description: ALB allow HTTP 80 from Internet

VPC: your working VPC.

Inbound rules → Add rule

Type: HTTP

Port range: 80

Source: 0.0.0.0/0 (optionally ::/0 if using IPv6)

Outbound rules: keep the default All traffic (0.0.0.0/0).

![SG](/ThuanWS/images/6-SG_for_ALB&Services/3.png) 

Then, click "Create security group".

## SG cho service Linux (ecs-linux-sg)
Go to EC2 → Security Groups → Create security group.

Security group name: ecs-linux-sg

Description: Allow ALB to Linux service on port 5000

VPC: same VPC as ALB.

Inbound rules → Add rule

Type: Custom TCP

Port range: 5000

Source: Custom → Security group, then select alb-sg (search by sg-... or name).

Important: the source must be SG alb-sg, not 0.0.0.0/0.

Outbound rules: keep default All traffic.

![SG](/ThuanWS/images/6-SG_for_ALB&Services/4.png) 

Tags → Add tag: Name = ecs-linux-sg. Then, click "Create security group".

![SG](/ThuanWS/images/6-SG_for_ALB&Services/5.png) 

## SG cho service Windows (ecs-win-sg)
Similar to make linux ecs-linux-sg, just some changes

![SG](/ThuanWS/images/6-SG_for_ALB&Services/6.png) 

Below is the result we get after creating the SecurityGroups

![SG](/ThuanWS/images/6-SG_for_ALB&Services/7.png) 