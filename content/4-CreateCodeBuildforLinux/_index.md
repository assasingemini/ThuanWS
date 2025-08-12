---
title : "Create CodeBuild for Linux"
date: 2025-08-07
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
## Create CodeBuild for Linux

Vào AWS CodeBuild → Create build project. Project name: build-linux.

![linux](images/4-CreateCodeBuildforLinux/1.png) 

![linux](images/4-CreateCodeBuildforLinux/2.png) 

![linux](images/4-CreateCodeBuildforLinux/3.png) 

In Source provider we will choose GitHub. You can connect Github account with AWS as follows:

![linux](images/4-CreateCodeBuildforLinux/4.png) 

![linux](images/4-CreateCodeBuildforLinux/5.png) 

![linux](images/4-CreateCodeBuildforLinux/6.png) 

![linux](images/4-CreateCodeBuildforLinux/7.png) 

![linux](images/4-CreateCodeBuildforLinux/8.png) 

Here you will enter the password of your GitHub account

![linux](images/4-CreateCodeBuildforLinux/10.png) 

![linux](images/4-CreateCodeBuildforLinux/11.png) 

![linux](images/4-CreateCodeBuildforLinux/12.png) 

After doing the above steps, we can go back to the source section and select as shown.

![linux](images/4-CreateCodeBuildforLinux/13.png)

Scroll down to the environment and we will configure it as shown in the picture:

![linux](images/4-CreateCodeBuildforLinux/14.png)

![linux](images/4-CreateCodeBuildforLinux/15.png)

Then in the Buildspec section, do as shown in the picture:

![linux](images/4-CreateCodeBuildforLinux/16.png)

Finally, Artifact and Logs will be configured as shown below and we will click on Create build project

![linux](images/4-CreateCodeBuildforLinux/17.png)

This is the message after the project build is successful

![linux](images/4-CreateCodeBuildforLinux/18.png)

## Gán quyền IAM cho CodeBuild

Go to IAM → Roles

![linux](images/4-CreateCodeBuildforLinux/19.png)

Find the newly created role for CodeBuild

![linux](images/4-CreateCodeBuildforLinux/20.png)

Attach policy: AmazonEC2ContainerRegistryPowerUser

![linux](images/4-CreateCodeBuildforLinux/21.png)

![linux](images/4-CreateCodeBuildforLinux/22.png)

Then we will go back to CodeBuild to run build-linux

![linux](images/4-CreateCodeBuildforLinux/23.png)

Bấm vào Start build nếu thành công sẽ có kết quả như hình bên dưới

![linux](images/4-CreateCodeBuildforLinux/24.png)

Click Start build if successful, the result will be as shown below.

![linux](images/4-CreateCodeBuildforLinux/25.png)

![linux](images/4-CreateCodeBuildforLinux/26.png)