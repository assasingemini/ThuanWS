---
title : "Clone repo & đẩy mã nguồn"
date: 2025-08-07
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
### Mục tiêu
Đưa bộ mã mẫu đa nền tảng vào repo.

### Các file bắt buộc
app.py (+ requirements.txt have Flask==3.0.3)

![clone](/ThuanWS/images/2-Clonerepo&pushsource/apppyfile.png) 

![clone](/ThuanWS/images/2-Clonerepo&pushsource/requirementtxt.png) 

main.ps1 

![clone](/ThuanWS/images/2-Clonerepo&pushsource/mainps1.png) 

Dockerfile.linux, Dockerfile.windows

![clone](/ThuanWS/images/2-Clonerepo&pushsource/dockerfilelinux.png) 

![clone](/ThuanWS/images/2-Clonerepo&pushsource/docketfilewindows.png) 

buildspec-linux.yml, buildspec-windows.yml

![clone](/ThuanWS/images/2-Clonerepo&pushsource/buildspeclinux.png) 

![clone](/ThuanWS/images/2-Clonerepo&pushsource/buildspecwindows.png) 

### Lệnh

git add -A
git commit -m "Add Dockerfiles, buildspecs, Linux & Windows apps"
git push -u origin main

![clone](/ThuanWS/images/2-Clonerepo&pushsource/gitpush.png)

![clone](/ThuanWS/images/2-Clonerepo&pushsource/pushfinish.png)