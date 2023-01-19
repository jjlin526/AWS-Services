### Database Services and Utilities

### AWS Databases and Related Services

![image](https://user-images.githubusercontent.com/114364831/213524147-2f98ac0a-503f-4d78-a628-55ee016cc950.png)

### Cloud Computing Models

![image](https://user-images.githubusercontent.com/114364831/213524987-f5c6466d-de53-4027-b82d-44b0ca14e826.png)

* If you are a DevOps engineer that wants complete control over OS that database is running on, can use EC2 directly
* If want control over database but not control over underlying infrastructure -- leverage Relational Database Service (RDS)
* SaaS approaches such DynamoDB, Elasticache and Redshift

### Overview

* Review the cloud computing models for databases on AWS
* Introduce the Relational Database Service (RDS)
* Examine the capabilities of Amazon Aurora (option within RDS)
* Introduce the DynamoDB service
* Review the Elasticache service
* Examine data warehousing of data on AWS

### Amazon Relational Database Service

* Takes a PaaS approach to running databases that we can leverage within our apps that are running on the platform
* Fully managed service for relational databases
* Handles provisioning, patching, backup, and recovery of your database (requires fair amount of time to implement and a lot of automation to integrate it in without the service)
* Supports deployment across multiple availability zones (multi-AZ)
* Some platforms support read replicas (scale out your data)
* Launches into a VPC
* Provides both general purpose SSD and provisioned IOPS SSD drive options
