---
title : "Cross-Platform DevOps with Windows and Linux Environments"
date: 2025-08-07
weight : 1 
chapter : false
---
# Cross-Platform DevOps with Windows and Linux Environments

**Lab Objectives**
This lab helps you get familiar with and practice building a cross-platform DevOps workflow on AWS, supporting deployment of applications on both Windows and Linux environments. You will learn how to use basic AWS services to automate building, deploying cross-platform applications, and test the results.

**Benefits of this Lab**
- Understand practical cross-platform DevOps workflows.
- Practice building Linux and Windows Docker images with CodeBuild and pushing them to Amazon ECR.
- Get familiar with popular AWS services used in DevOps.
- Develop skills to automate application deployment on the cloud.

**Key AWS Services Used**
- GitHub (via AWS CodeConnections) - Git source code repository
- AWS CodeBuild - Build source and create Docker images
- Amazon ECR (Elastic Container Registry) - Store and manage Docker images
- AWS CodePipeline - Automate build and push for Linux and Windows
- Application Load Balancer - Path-based routing to Linux and Windows EC2

![cấu trúc](/ThuanWS/images/pic.png) 

*The diagram shows the target architecture from the project proposal. This lab implements the CI pipeline (build and push images) and ALB routing to Linux/Windows EC2.*

### Content
1. [Create GitHub repository](1-GitHub_repository/)
2. [Clonerepo & pushsource](2-Clonerepo&pushsource/)
3. [Create ECR repositoriesn](3-CreateECRrepositories/)
4. [Create CodeBuild for Linux](4-CreateCodeBuildforLinux/)
5. [Create CodeBuild for Windows](5-CreateCodeBuildforWindows/)
6. [Create Security Groups (SG) for ALB & Services](6-SG_for_ALB&Services/)
7. [Create and Configure Windows EC2 Target Group with ALB](7-ConfigureandVerifyWindowsEC2ConnectiontoALBviaTargetGroup/)
8. [Create CodePipeline for Linux and Windows](8-CreateCodePipeline/)
9. [Clean Up AWS Resources](9-CleanUpAWSResources/)
