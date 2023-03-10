### Compute Services

* A service that enables you to leverage **cloud-based virtual machines** for workloads. This could be serving web content to visitors, running a database, or calculating statistics from a data set.

### Compute Services on AWS

![image](https://user-images.githubusercontent.com/114364831/212352909-bc4954a7-7e9a-4ee3-9aed-94655e0c1501.png)

### Amazon EC2 Overview
 
Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides resizable compute capacity in the cloud. It is designed to make web-scale computing easier for developers.

### Amazon EC2 Use Cases

* **Web application hosting** - spin up an EC2 instance, install web server on instance, put files for web app on web server
* **Batch processing** - do preprocessing on millions of rows of POS data
* **Web services endpoint** - API server; take web services and launch them in the cloud for other apps to access
* **Desktop in the cloud** - launch Windows instance on Amazon EC2 and connect to it through Remote Desktop

### Amazon EC2 Concepts

![image](https://user-images.githubusercontent.com/114364831/212366239-a6b943b8-3140-472a-8f12-1cd376d45d94.png)

### Auto Scaling and Horizontal Scaling

* **Amazon EC2 Auto Scaling** is a service that automatically adds or removes EC2 instances from a group based on user-defined policies and health checks. It enables you to maintain application availability and scale your Amazon EC2 capacity up or down automatically according to conditions you define.
* **Horizontal scaling**, also called "scaling out," is the process of adding more resources (such as adding more servers) to a system to handle increased load. This is in contrast to "scaling up," which is the process of increasing the capacity of existing resources (such as upgrading a server with more memory or a faster CPU).
* Auto Scaling is a way to automatically increase the number of Amazon EC2 instances in a group as the demand for instances increases, and decrease the number of instances as the demand decreases. This is a form of horizontal scaling.

### Amazon EC2 Instance Types

* Defines the processor, memory, and storage type
* Cannot be changed without downtime
* Provided in the following categories:
  * General purpose (for most workloads)
  * Compute, memory, and storage optimized
  * Accelerated computing (for ML, with access to GPU)
* Pricing is based on instance type (specialized costs more than general purpose)
* Some instance types have unique capabilities (some instance families have access to specialized storage or access to GPU)

### Example EC2 Instance Type Pricing (i.e. us-east-1)

![image](https://user-images.githubusercontent.com/114364831/212369350-26b8baa6-42ca-440b-accd-7749eddbcc1c.png)

* t3.medium and m5.large are general-purpose instance types
* t3 
  * T3 instances are the low cost burstable general purpose instance type that provide a baseline level of CPU performance with the ability to burst CPU usage at any time for as long as required. T3 instances are designed for applications with moderate CPU usage that experience temporary spikes in use.
* c5d.24xlarge is a **compute-optimized** instance type
* p3.16xlarge is a very specialized instance type from the **accelerated computing** category which provides access to industry-leading GPUs for machine learning workflows. Although it appears to have less virtual CPUs, it has special capabilities in the p3 instance type family.
* i3.16xlarge is a storage-optimized instance type - has special access to storage capabilities

### Root Device Type

![image](https://user-images.githubusercontent.com/114364831/212370984-a509eff1-ba61-4aee-ac5d-a74784a41e2f.png)

- Instance Store: if you shut down the server, the data is gone (ephemeral)
- Elastic Block Store (EBS): if you shut down the server, the data is still there (persistent)
- EBS should be used for most work done with EC2

### Amazon Machine Image (AMI)

* **Template for an EC2 instance** including configuration, operating system, and data
* AWS provides many AMI's that can be leveraged (many AMI's provided by AWS that are easy to spin up an instance from)
* AMI's can be shared across AWS accounts
* Custom AMI's can be created based on your configuration
* Commercial AMI's are available in the AWS Marketplace

### Amazon EC2 Purchase Options

![image](https://user-images.githubusercontent.com/114364831/212372667-72ab2157-4255-4e3e-82e0-e5d9d97813b8.png)

### EC2 Reserved Instance Types

![image](https://user-images.githubusercontent.com/114364831/212372922-048086c4-1d57-4b1c-8830-371cba2209f8.png)

* Companies choose **Reserved Instances** because they come with substantial discounts compared to pay-as-you-go On-Demand pricing. All it takes is committing to a specified cloud capacity for a specified period of time. In AWS, it is one year or three years.

### Standard Reserved Instance Cost Models

![image](https://user-images.githubusercontent.com/114364831/212373112-c4281578-6ec0-4fb5-87d8-2cb7e4c6fc96.png)

### Savings Plans

* Similar in concept to reserved instances
* Supports compute with EC2, Fargate, and Lambda
* Unlike Reserved Instances, it does not reserve capacity
* Provide savings of up to 72%
* Comes in 1 or 3 year terms

### Spot Instances

* **Spot instances** enable you to leverage excess EC2 compute capacity (that might exist within an AZ)
* Can provide up to 90% discount over on-demand pricing
* There is a market price for isntnace types per availability zone called the **Spot price**
* When you request instances, if your bid is higher than the Spot price, they will launch
* If the Spot price grows to exceed your bid, the instances will be terminated 
* Spot instances can be notified 2 minutes prior to termination
* Use case: workloads that can start and stop without affecting what you are trying to do

### Dedicated Host

* The dedicated host pricing model gives you a dedicated physical server. It will be the most expensive option, but it may be required for either
  * Server software licensing
    * Dedicated Hosts are required when using certain types of server software licenses, such as those that are based on the physical characteristics of the server, rather than the number of instances or cores. This is because these types of licenses are tied to the physical server, and cannot be used with instances running on shared hosts.
  * Compliance requirement

### Amazon EC2 Purchase Options

![image](https://user-images.githubusercontent.com/114364831/212376746-f6e8be3e-d8ba-4f32-a45d-1a3ce5e15bc2.png)

![image](https://user-images.githubusercontent.com/114364831/212389190-59b1cedd-8b04-4ebd-943e-1a605dc7aa90.png)

### Reserved Instance EC2 Pricing Example

![image](https://user-images.githubusercontent.com/114364831/212390276-644429c1-ffc0-4927-a043-4489ef1ffe63.png)

### Spot Instance EC2 Pricing Example

![image](https://user-images.githubusercontent.com/114364831/212390697-1712484f-2df9-4340-bc2d-9aac80402a67.png)

### AWS Elastic Beanstalk

* Automates the process of deploying and scaling workloads on EC2 (PaaS; not IaaS because it does not deal with the servers directly)
* Supports a specific set of technologies
* Leverages existing AWS services
* Only pay for the other services you leverage
* Handles **provisioning, load balancing, scaling, and monitoring**

### Support Application Platforms

* Java
* .NET
* PHP
* Node.js
* Python
* Ruby
* Go
* Docker

### Elastic Beanstalk Features

![image](https://user-images.githubusercontent.com/114364831/212394997-906d7dd1-518e-49cd-80a2-c5617d34ccca.png)

### Use Cases

* Deploy an application with minimal knowledge of other services (i.e. know Elastic Beanstalk (EB) but not familiar with administering EC2 servers, auto scaling groups, getting metrics from CloudWatch, setting scaling rules, etc.)
* Reduce the overall maintenance needed for the application
* Few customizations needed (i.e. if need specific AMI, need specific package and do not want to upgrade to another version of the package, then use EC2 directly - not EB)

### AWS Lambda Overview

* AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume. You can run code for virtually any type of service - all with zero administration.

### AWS Lambda

* Enables the running of code without provisioning infrastructure
* Only charged for usage based on execution time
* Can configure available memory from 128 MB to 3008 MB
* Integrates with many AWS services (i.e. S3, DynamoDB)
* Enables **event-driven workflows** (i.e. when I upload a file, execute this function)
* Primary service for **serverless architecture**

### AWS Lambda Advantages

* Reduced maintenance requirements
* Enables fault tolerance without additional work (runs across multiple AZ's - no single point of failure can take down the app -- built into Lambda)
* Scales based on demand 
* Pricing is based on usage (i.e. but for EC2, a server supports 1 000 people but only 10 people using it - still have to pay for whole server -- Lambda maps to direct usage)

### Scenario Review

1. Sylvia's company is in the process of moving multiple workloads into AWS. One workload is an application that will be leveraged for at least 5 more years. The organization is looking to be as cost efficient as possible for its EC2 usage. What EC2 purchase option should be chosen for this application?

* All Upfront Reserved - 3 Years

2. Edward is looking to deploy his PHP web application to a virtual server. He does not have experience managing EC2 instances on AWS. He needs the ability to scale this application to meet user demand. What is the best compute option for Edward based on this crtieria?

* AWS Elastic Beanstalk (EB) -- supports PHP and handles scaling

3. Cindy's company is transitioning to the cloud for its data processing workloads. The workloads happen daily and can start or stop without a problem. This workload will be leveraged for at least one year. What EC2 purchase option would be the most cost efficient choice?

* Spot Instances 
-- can start or stop without a problem (always spot instance - most cost efficient)
