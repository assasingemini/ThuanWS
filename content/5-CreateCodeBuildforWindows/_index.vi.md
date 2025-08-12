---
title : "Tạo CodeBuild cho Windows"
date: 2025-08-07
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
## Mục tiêu
Xây dựng một ảnh container Windows từ Dockerfile.windows và đẩy nó lên Amazon ECR (us-east-1) bằng AWS CodeBuild (Windows – Chế độ phiên bản).

## Điều kiện tiên quyết
Kho GitHub của bạn chứa: Dockerfile.windows, main.ps1 và buildspec-windows.yml (tại thư mục gốc của kho).

Tên kho ECR: windows-app trong us-east-1 (buildspec có thể tự động tạo).

Vai trò dịch vụ CodeBuild có quyền ECR — dễ nhất: AmazonEC2ContainerRegistryPowerUser.

## Tạo dự án CodeBuild cho Windows
Chúng ta cũng sẽ làm tương tự khi tạo CodeBuild cho Linux

Trước tiên, hãy vào CodeBuild, đặt tên là build-windows, cấu hình như hình dưới đây, những phần còn lại sẽ tương tự như cấu hình cho build-linux

![windows](images/5-CreateCodeBuildforWindows/1.png) 

![windows](images/5-CreateCodeBuildforWindows/2.png) 

![windows](images/5-CreateCodeBuildforWindows/3.png) 

![windows](images/5-CreateCodeBuildforWindows/4.png) 

![windows](images/5-CreateCodeBuildforWindows/5.png) 

Sau khi tạo dự án thành công, chúng ta sẽ cấp quyền ECR cho vai trò CodeBuild.

![windows](images/5-CreateCodeBuildforWindows/6.png)

![windows](images/5-CreateCodeBuildforWindows/7.png)

![windows](images/5-CreateCodeBuildforWindows/8.png)

![windows](images/5-CreateCodeBuildforWindows/9.png)

Cuối cùng chúng ta sẽ quay lại CodeBuild để xây dựng dự án build-windows

![windows](images/5-CreateCodeBuildforWindows/10.png)

![windows](images/5-CreateCodeBuildforWindows/11.png)

Sau khi xây dựng, hãy quay lại ecr. Nếu window-apps có thẻ hình ảnh với phần mở rộng "latest" thì đã thành công.

![windows](images/5-CreateCodeBuildforWindows/12.png)
