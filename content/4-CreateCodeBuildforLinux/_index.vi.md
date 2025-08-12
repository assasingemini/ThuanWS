---
title : "Tạo CodeBuild cho Linux"
date: 2025-08-07
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
## Tạo CodeBuild cho Linux

Vào AWS CodeBuild → Create build project. Project name: build-linux.

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/1.png) 

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/2.png) 

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/3.png) 

Ở Source provider chúng ta sẽ chọn GitHub. Bạn có thể kết nối Github account với AWS như sau:

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/4.png) 

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/5.png) 

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/6.png) 

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/7.png) 

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/8.png) 

Ở đây bạn sẽ nhập mật khẩu của tài khoản GitHub của mình

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/10.png) 

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/11.png) 

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/12.png) 

Sau khi làm các bước ở trên chúng ta có thể quay trở lại phần source và chọn theo như hình

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/13.png)

Kéo xuống environment chúng ta sẽ cấu hình như trong hình:

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/14.png)

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/15.png)

Sau đó ở phần Buildspec sẽ làm theo như trong hình:

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/16.png)

Cuối cùng Artifact và Logs sẽ cấu hình như hình bên dưới và chúng ta sẽ bấm vào Create build project

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/17.png)

Đây là thông báo sau khi build project thành công

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/18.png)

## Gán quyền IAM cho CodeBuild

Vào IAM → Roles

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/19.png)

Tìm role vừa tạo cho CodeBuild

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/20.png)

Attach policy: AmazonEC2ContainerRegistryPowerUser

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/21.png)

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/22.png)

Sau đó chúng ta sẽ quay về CodeBuild để chạy build-linux

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/23.png)

Bấm vào Start build nếu thành công sẽ có kết quả như hình bên dưới

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/24.png)

Sau đó chúng ta vào ECR → linux-app → Images để kiểm tra image đã push thành công

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/25.png)

![linux](/ThuanWS/images/4-CreateCodeBuildforLinux/26.png)