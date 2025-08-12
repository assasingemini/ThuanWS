---
title : "Tạo repository trên ECR"
date: 2025-08-07
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
## Tạo repository cho ứng dụng Linux

Truy cập Amazon ECR trong AWS Management Console.

![ecr](/ThuanWS/images/3-CreateECRrepositories/1.png) 

Chọn Private registry → Repositories → Create repository.

![ecr](/ThuanWS/images/3-CreateECRrepositories/2.png) 

Trong mục General settings, nhập tên repository: linux-app

Trong phần Image tag settings, giữ nguyên mặc định là Mutable.

Trong phần Encryption settings, giữ nguyên mặc định AES-256.

Nhấn Create repository.

![ecr](/ThuanWS/images/3-CreateECRrepositories/3.png) 

Kết quả chúng ta có được:

![ecr](/ThuanWS/images/3-CreateECRrepositories/4.png) 

## Tạo repository cho ứng dụng Windows

Lặp lại các bước trên nhưng đổi tên repository thành: windows-app

Sau khi hoàn thành, trong Repositories sẽ xuất hiện 2 repository:

![ecr](/ThuanWS/images/3-CreateECRrepositories/5.png) 

