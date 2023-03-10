### File Storage Services

### AWS File Storage and Data Transfer Services

![image](https://user-images.githubusercontent.com/114364831/212757260-e1e99132-fb67-4d56-a814-37768664955b.png)

### Overview

### Amazon Simple Storage Service (S3)

* Stores files as objects in buckets
    * Buckets are the unit of organization within S3. You will create a bucket with a set of settings; any file that you drop in has those settings applied to it.
* Provide different storage classes for different use cases
* Stores data across multiple availability zones (durability and resiliency for data)
* Enables URL access for files
* Offers configurable rules for data lifecycle
    * If you want something to expire after a given time or go to a different storage class
* Can serve as a static website host

### Amazon S3 Non-archival Storage Classes

![image](https://user-images.githubusercontent.com/114364831/212760937-bd28347d-23ac-4aa4-9c3e-9d77116931c4.png)

### S3 Intelligent Tiering Storage Class

* Automatically move files based on access
* Moves between frequent and infrequent access
* Same performance as S3-Stanard (can provide cost savings if you have some data that needs to be moved between storage classes)

### S3 Lifecycle Policies

* Objects in a bucket can transition or expire based on your criteria (cannot move an object back on forth based on usage -- only available with **Intelligent Tiering**)
* Transitions can enable objects to move to another storage based on time (i.e. can configure a certain file to last for 30 days based on **Lifecycle Policies**)
* Expiration can delete objects based on age 
* Policies can also factor in versions of a specific object in the bucket (i.e. can delete a version of the file that is not the current version after 7 days)

### S3 Transfer Acceleration

* Feature that can be enabled per bucket that allows for optimized uploading of data using the AWS Edge Locations are part of Amazon CloudFront -- (upload data in a fast and efficient way into S3 buckets)

### Hosting a Website on Amazon S3

* Create a new S3 bucket
* Upload objects to an S3 bucket
* Access objects from S3 bucket from URL
* Configure a bucket for website hosting

### Glacier and Glacier Deep Archive

### Amazon S3 Glacier

* Designed for archiving of data within S3 as separate storage classes
* Offers configurable retrieval times (higher cost to retrieve faster)
* Can send files directly or through lifecycle rules in S3 (i.e. to transition data into S3 Glacier)
* Provides two different storage classes
   * S3 Glacier
   * S3 Glacier Deep Archive

### Amazon S3 Glacier Storage Classes

### S3 Glacier  

* Designed for archival data
* 90 day minimum storage duration change
* Can be retrieved in either minutes or hours
* You pay a retrieval fee per GB retrieved (in addition to storage cost, pay to retrieve it)
* Over 5 times less expensive than S3 Standard storage class (compelling reason to utilize it if data will not be accessed except for rare circumstances)

### S3 Glacier Deep Archive

* Designed for archival data
* 180 day minimum storage duration change
* Can be retrieved in hours
* You pay a retrieval fee per GB retrieved
* Over 23 times less expensive than S3 Standard storage class

### S3 Glacier Setup

* The AWS Management Console can be used to quickly set up Amazon S3 Glacier. Data can then be uploaded and retrieved programatically (CLI or SDK) -- situation in which certain things cannot be done in the console

### Elastic Block Store (EBS)

### Amazon EC2 File Storage Services

![image](https://user-images.githubusercontent.com/114364831/213287437-55ca8e6b-a8e1-4be7-a421-3f740fb90079.png)

* EFS is a network file system designed for Linux-based workloads

### Amazon Elastic Block Store (EBS)

* Block storage designed to be connected to a single EC2 instance that can scale to support petabytes of data and support multiple volume types based on need.

### Amazon EBS

* Enables redundancy within an AZ (durability)
* Allows users to take snapshots of data (data on a drive attached to EC2 instance can periodically be backed up)
* Offers encryption of its volumes (does not encrypt by default)
* Provides multiple volume types:
   * General purpose SSD
   * Provisioned IOPS SSD
   * Throughput optimized HDD
   * Cold HDD

### Amazon EBS Volume Types

![image](https://user-images.githubusercontent.com/114364831/213289143-0a591768-4b65-436a-ba5c-26c13cb3e612.png)

### Elastic File System

* Fully managed Network File System (NFS)
* Designed for Linux workloads
* Supports up to petabyte scale
* Stores data across multiple AZ's
* Provides two different storage classes
   * Standard
   * Infrequent access
* Provides configurable lifecycle data rules (transition between storage classes)

### EFS Example

![image](https://user-images.githubusercontent.com/114364831/213291495-205232f8-1015-4aa7-be25-d1ab17a6ec59.png)

* EFS has the ability to be a network file system that attaches to multiple EC2 instances at the same time (EBS can only attach to a single EC2 instance) -- EFS has a mount point within each AZ

### Amazon FSx for Windows File Server

* Fully managed native Windows file system (as opposed to Linux file system with EFS)
* Includes native Windows features including:
   * **SMB support** (allows devices to access and share files and resources over the network using the SMB protocol)
   * **Active Directory** integration (a directory service that authenticates and authorizes all users and computers in a Windows domain type network, and it is an integral part of the Windows operating system)
   * **Windows NFTS** (New Technology File System -- a file system that is used by the Windows operating system to store and manage files. It provides advanced features such as file and folder permissions, encryption, and disk quotas)
* Utilizes SSD drives for low latency

### Data Transfer with AWS Snowball

### AWS Large Scale Data Transfer Services

![image](https://user-images.githubusercontent.com/114364831/213296139-2c8627d2-8afa-4515-955f-003795458589.png)

### Large-scale Data Transfer into AWS

### AWS Snowball

* Designed for large-scale data transfer
* Supports petabyte scale transfer
* Physical device is delivered by AWS
* You connect the Snowball to your network and upload your data
* Device is returned by local carrier
* AWS receives device and loads your data into S3

### AWS Snowmobile

* Designed for large-scale data transfer
* Supports exabyte scale transfer
* Ruggedized shipping container is delivered to your location
* AWS sets up a connection to your network (from shipping container)
* You load your data on the Snowmobile
* AWS will load data into S3 when the container is received at an AWS location

### Summary

* Reviewed the storage services on AWS
* Examined Amazon S3 and its capabilities
* Implemented a static website on Amazon S3
* Explored archive capabilities with Glacier and Glacier Deep Archive
* Reviewed EC2 storage leveraging EBS and EFS
* Examined large-scale data transfer services into AWS

### Scenario-based Review  

### Scenario 1

Elaine launched a site that offers daily tutorials for developers. She uses S3 to store the assets needed per tutorial. These assets are very popular within the week the tutorial is launched. After this initial week, these assets are rarely accessed. How could Elaine reduce her S3 costs while maintaining durability?

* **S3 lifecycle rules with S3-Standard Infrequent Access (IA) storage class** (S3 lifecycle rules - assets are only popular within the week the tutorial is launched -- define policy that changes storage class of data after 7 days of being placed in the S3 bucket; S3-Standard IA storage class because data is not frequently accessed, not One Zone-IA in order to maintain durability of data)

### Scenario 2

Esteban works for a social networking company and they are moving to AWS. They have 2 PB of user-generated content that they need to migrate. Esteban is trying to determine if there is a faster way than uploading over the internet. Would there be another approach for Esteban's company?

* **AWS Snowball** (need AWS Snowmobile for exabytes of data)

### Scenario 3

Emily works for a company that produces a message app. She is looking for a shared file system between 8 different Linux EC2 instances. The file system would need to support roughly 1 PB of data. What approach would you recommend for Emily?

* **Amazon Elastic File System** (needs to be for Linux instances and needs to be for petabytes of data or less, not in exabytes)

