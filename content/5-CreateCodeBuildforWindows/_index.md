---
title : "Create CodeBuild for Windows"
date: 2025-08-07
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
## Goal
Build a Windows container image from Dockerfile.windows and push it to Amazon ECR (us-east-1) using AWS CodeBuild (Windows – Instance mode).

## Prerequisites
Your GitHub repo contains: Dockerfile.windows, main.ps1, and buildspec-windows.yml (at repo root).

ECR repository name: windows-app in us-east-1 (the buildspec can auto-create it).

CodeBuild service role has ECR permissions — easiest: AmazonEC2ContainerRegistryPowerUser.

## Create the CodeBuild project for Windows
We will also do almost the same with creating CodeBuild for Linux

First go to CodeBuild, name it build-windows, configure as shown below, the rest will be similar to the configuration for build-linux

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/1.png) 

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/2.png) 

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/3.png) 

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/4.png) 

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/5.png) 

After successfully creating the project, we will grant ECR permissions to CodeBuild role.

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/6.png)

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/7.png)

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/8.png)

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/9.png)

Finally we will go back to CodeBuild to build the build-windows project

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/10.png)

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/11.png)

After building, go back to ECR. If window-apps has an image tag with the latest extension, it is successful.

![windows](/ThuanWS/images/5-CreateCodeBuildforWindows/12.png)