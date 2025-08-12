---
title : "Tạo CodePipeline cho Linux và Windows"
date: 2025-08-07
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---
## Mục tiêu
Tự động hóa quy trình build và deploy ứng dụng Linux và Windows từ GitHub lên ECS thông qua AWS CodePipeline, sử dụng CodeBuild đã tạo trước đó.

## Chọn Template

Vào AWS Console → tìm CodePipeline → chọn Create pipeline.

Ở mục Category, chọn Deployment.

Trong phần Template, chọn Push to ECR.

![pline](/ThuanWS/images/8-CreateCodePipeline/1.png) 

## Chọn Nguồn

Source provider: chọn GitHub (via GitHub App).

Nhấn Connect to GitHub (nếu chưa có connection).

Chọn repository chứa mã nguồn (VD: assasignemini/devops-crossplatform).

Chọn branch main.

Giữ Output artifact format là CodePipeline default.

Bấm Next.

![pline](/ThuanWS/images/8-CreateCodePipeline/2.png) 

## Cấu hình Template

CodePipelineName: đặt tên pipeline (VD: linux-pipeline hoặc windows-pipeline).

DockerBuildContext: .

DockerFilePath: ./Dockerfile

ImageTag: latest

RetentionPolicy: chọn Delete để xoá tài nguyên phụ trợ khi xoá stack.

Bấm Create pipeline from template để hoàn tất.

![pline](/ThuanWS/images/8-CreateCodePipeline/3.png) 

##  Kết quả sau khi tạo Pipeline

Pipeline hiển thị 2 stage:

Source: Lấy code từ GitHub qua CodeConnections.

Build_and_Deploy: Build Docker image và push lên ECR.

Màu xanh báo thành công, xanh dương báo đang chạy.

Nếu không muốn build tốn tài nguyên, có thể bấm Stop execution ngay sau khi tạo.

Hình dưới đây là chỉ mới tạo pipeline cho Linux

![pline](/ThuanWS/images/8-CreateCodePipeline/4.png) 

Để tạo pipeline cho Windows, thực hiện giống pipeline Linux nhưng ở Template Details (Step 3) đặt CodePipelineName là windows-pipeline, chọn:

DockerBuildContext: .

DockerFilePath: ./Dockerfile.windows

Chọn ECR repository cho Windows (nếu có).