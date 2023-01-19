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

### Amazon RDS Platforms

* MySQL
* PostgreSQL
* MariaDB
* Oracle Database
* SQL Server
* Amazon Aurora (created in the beginning to work on RDS)

### Amazon Aurora

* Amazon Aurora is a MySQL and PostgreSQL-compatible relational database built for the cloud, that combines the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases

### Amazon Database Migration Service (DMS)

* Enables you to move data into AWS from existing databases
* Supports both one time and continual migration of data
* Supports many popular commercial and open source databases
* Only pay for compute leveraged in the migration process

### Amazon DynamoDB 

* Fully managed NoSQL database service (you do not manage underlying infrastructure or database layer -- simply use database; NoSQL provides more flexibility in terms of schema but provides other limitations)
* Provides both **key-value** and **document** database
* Enables extremely low latency at virtually any scale (built for Amazon.com)
* Supports automated scaling based on configuration (i.e. based on predicted need, but can also scale automatically based on usage)
* Offers **in-memory cache** with the **DynamoDB Accelerator (DAX)**
  * An in-memory cache is a way to temporarily store frequently accessed data in memory, rather than fetching it from the database each time it is needed. This can significantly improve performance by reducing the number of database queries and the latency of each query. The cache is typically implemented using a data structure such as a hash table or a linked list, and it is usually managed by a caching library or framework. The cache is usually implemented on the application side.
  * DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for DynamoDB that delivers up to a 10x performance improvement. DAX read and write requests are fully compatible with DynamoDB, so you can use your existing DynamoDB API calls with DAX.
