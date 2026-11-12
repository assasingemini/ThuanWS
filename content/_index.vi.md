---
title : "Triển khai DevOps đa nền tảng cho môi trường Windows và Linux"
date: 2025-08-07
weight : 1 
chapter : false
---
# Triển khai DevOps đa nền tảng cho môi trường Windows và Linux

**Mục tiêu lab**
Lab này giúp bạn làm quen và thực hành xây dựng quy trình DevOps đa nền tảng trên AWS, hỗ trợ triển khai ứng dụng trên cả môi trường Windows và Linux. Bạn sẽ học cách sử dụng các dịch vụ AWS cơ bản để tự động hóa việc build, deploy ứng dụng đa nền tảng và kiểm thử kết quả.

**Lợi ích**
- Hiểu được quy trình DevOps đa nền tảng thực tế.
- Thực hành build Docker image cho Linux và Windows bằng CodeBuild và đẩy lên Amazon ECR.
- Làm quen với các dịch vụ AWS phổ biến phục vụ DevOps.
- Phát triển kỹ năng tự động hóa triển khai ứng dụng trên đám mây.

**Các dịch vụ chính sử dụng**
- GitHub (kết nối qua AWS CodeConnections) - Kho lưu trữ mã nguồn
- AWS CodeBuild - Build mã nguồn và tạo Docker image 
- Amazon ECR (Elastic Container Registry) - Lưu trữ và quản lý Docker images 
- AWS CodePipeline - Tự động build và đẩy image cho Linux và Windows
- Application Load Balancer - Định tuyến theo đường dẫn tới EC2 Linux và Windows

![cấu trúc](/ThuanWS/images/pic.png) 

*Sơ đồ thể hiện kiến trúc mục tiêu trong Project Proposal. Lab này thực hiện phần pipeline build/đẩy image và ALB định tuyến tới EC2 Linux/Windows.*

### Nội dung
1. [Tạo Git Hub repository](1-GitHub_repository)
2. [Clone repo & đẩy mã nguồn](2-Clonerepo&pushsource/)
3. [Tạo repository trên ECR](3-CreateECRrepositories/)
4. [Tạo CodeBuild cho Linux](4-CreateCodeBuildforLinux/)
5. [Tạo CodeBuild cho Windows](5-CreateCodeBuildforWindows/)
6. [Tạo Security Groups (SG) cho ALB & Services](6-SG_for_ALB&Services/)
7. [Tạo và cấu hình Target Group cho Windows EC2 với ALB](7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/)
8. [Tạo CodePipeline cho Linux và Windows](8-CreateCodePipeline/)
9. [Dọn dẹp tài nguyên AWS](9-CleanUpAWSResources/)
