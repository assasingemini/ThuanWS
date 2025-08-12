---
title : "Create CodePipeline for Linux and Windows"
date: 2025-08-07
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---
## Objective
Automate the process of building and deploying Linux and Windows applications from GitHub to ECS via AWS CodePipeline, using a previously created CodeBuild.

## Select Template

Go to AWS Console → find CodePipeline → select Create pipeline.

In Category, select Deployment.

In Template, select Push to ECR.

![pline](/ThuanWS/images/8-CreateCodePipeline/1.png) 

## Select Source

Source provider: select GitHub (via GitHub App).

Click Connect to GitHub (if not connected yet).

Select the repository containing the source code (eg assasignemini/devops-crossplatform).

Select the main branch.

Keep Output artifact format as CodePipeline default.

Click Next.

![pline](/ThuanWS/images/8-CreateCodePipeline/2.png) 

## Template Configuration

CodePipelineName: name the pipeline (eg: linux-pipeline or windows-pipeline).

DockerBuildContext: .

DockerFilePath: ./Dockerfile

ImageTag: latest

RetentionPolicy: select Delete to delete the auxiliary resources when deleting the stack.

Click Create pipeline from template to finish.

![pline](/ThuanWS/images/8-CreateCodePipeline/3.png) 

## Results after creating Pipeline

Pipeline shows 2 stages:

Source: Get code from GitHub via CodeConnections.

Build_and_Deploy: Build Docker image and push to ECR.

Green indicates success, blue indicates running.

If you don't want to build to waste resources, you can click Stop execution right after creating.

The image below shows just creating a pipeline for Linux

![pline](/ThuanWS/images/8-CreateCodePipeline/4.png) 

To create a pipeline for Windows, do the same as the Linux pipeline but in Template Details (Step 3) set CodePipelineName to windows-pipeline, select:

DockerBuildContext: .

DockerFilePath: ./Dockerfile.windows

Select the ECR repository for Windows (if available).