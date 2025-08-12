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
- Master steps from coding, building Docker images to deploying on ECS.
- Get familiar with popular AWS services used in DevOps.
- Develop skills to automate application deployment on the cloud.

**Key AWS Services Used**
- AWS CodeCommit - Git source code repository
- AWS CodeBuild - Build source and create Docker images
- Amazon ECR (Elastic Container Registry) - Store and manage Docker images
- Amazon ECS Fargate - Serverless container deployment and running

![cấu trúc](/ThuanWS/images/pic.png) 

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