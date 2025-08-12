---
title : "Clean Up AWS Resources"
date: 2025-08-07
weight : 9 
chapter : false
pre : " <b> 9. </b> "
---
## Objective
Delete AWS resources created during the lab to avoid unnecessary costs.

## Delete Pipelines

Go to AWS Console → CodePipeline.

Select linux-pipeline and windows-pipeline.

Click Delete and confirm.

## Delete CodeBuild Projects

Go to AWS Console → CodeBuild.

Select build projects created by the pipeline (e.g. Docker_Build_Tag_and_Push).

Click Delete.

## Delete EC2 Instances and Security Groups

Go to AWS Console → EC2 → Instances.

Select Linux and Windows instances → Terminate.

Go to Security Groups, delete security groups created specifically for the lab (if not used for other services).

## Delete Target Groups and Load Balancer

Go to AWS Console → EC2 → Load Balancers, delete the lab's Application Load Balancer.

Go to Target Groups, delete linux-tg and windows-tg.

## Check Billing

Go to AWS Console → Billing → Bills.

Confirm that no services are running (EC2, ECR, CodeBuild, ALB…).