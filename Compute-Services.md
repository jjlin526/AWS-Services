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
