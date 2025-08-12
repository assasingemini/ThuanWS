---
title : "Dọn dẹp tài nguyên AWS"
date: 2025-08-07
weight : 9 
chapter : false
pre : " <b> 9. </b> "
---
## Mục tiêu
Xóa các tài nguyên AWS đã tạo trong quá trình làm lab để tránh phát sinh chi phí không cần thiết.

## Xóa Pipelines

Vào AWS Console → CodePipeline.

Chọn linux-pipeline và windows-pipeline.

Nhấn Delete và xác nhận.

##  Xóa CodeBuild Projects

Vào AWS Console → CodeBuild.

Chọn các project build được tạo bởi pipeline (ví dụ: Docker_Build_Tag_and_Push).

Nhấn Delete.

## Xóa EC2 Instances và Security Groups 

Vào AWS Console → EC2 → Instances.

Chọn instance Linux và Windows → Terminate.

Vào Security Groups, xóa các nhóm bảo mật tạo riêng cho lab (nếu không dùng cho dịch vụ khác).

## Xóa Target Groups và Load Balancer

Vào AWS Console → EC2 → Load Balancers, xóa Application Load Balancer của lab.

Vào Target Groups, xóa linux-tg và windows-tg.

## Kiểm tra Billing

Vào AWS Console → Billing → Bills.

Xác nhận không còn dịch vụ nào đang chạy (EC2, ECR, CodeBuild, ALB…).