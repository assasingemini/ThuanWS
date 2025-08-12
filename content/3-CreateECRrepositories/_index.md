---
title : "Create ECR repositories"
date: 2025-08-07
weight : 3
chapter : false
pre : " <b> 3. </b> "
---
## Create repository for Linux application

First, go to Amazon ECR in the AWS Management Console.

![ecr](images/3-CreateECRrepositories/1.png) 

Select Private registry → Repositories → Create repository.

![ecr](images/3-CreateECRrepositories/2.png) 

In the General settings section, enter repository name: linux-app

In the Image tag settings section, keep the default Mutable.

In the Encryption settings section, keep the default AES-256.

Click Create repository.

![ecr](images/3-CreateECRrepositories/3.png) 

The results we get.

![ecr](images/3-CreateECRrepositories/4.png) 

## Create repository for Windows application

Repeat the above steps but change the repository name to: windows-app

After completion, the Repositories list should show:

![ecr](images/3-CreateECRrepositories/5.png) 


