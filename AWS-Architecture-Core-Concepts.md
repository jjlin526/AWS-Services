### AWS Architecture Core Concepts

### Security and Architecture Overview

* Reviewing core concepts around security and architecture
* Exploring the AWS Shared Responsibility Model
* Introducing the AWS Well Architected Framework
* Examining fault tolerance and high availability on AWS
* Understanding provided tools for compliance

### Acceptable Use Policy

* AWS's policy for acceptable and unacceptable uses of their cloud platform. All users must agree with this policy to have an account on the platform.

### Acceptable Use Policy

* Sending unsolicited mass emails is prohibited
* Hosting or distributing harmful content is prohibited (viruses, malware, etc.)
* Penetration tests are allowed for a list of specific services (look for holes in security -- i.e. what ports are open on a specific server)

### Least Privilege Access

* When granting permissions for a user to access AWS resources, you should grant them the minimum permissions needed to complete their tasks and no more
  * Do not use root account by default - set up IAM account on daily basis (example of least privilege access)

### Shared Responsibility Model

* Security and Compliance is a shared responsibility between AWS and the customer

### Shared Responsibility Summary

![image](https://user-images.githubusercontent.com/114364831/214102258-474efaf6-10e5-47ea-8dbe-4918cc5807f2.png)

* AWS has the responsibility over the core systems that are running the platform
* Customer has control over the things they are putting onto the platform and how they are using it

### Shared Responsibility Model

### AWS Responsibility

* Access control and training for Amazon employees 
* Global data centers and underlying network (AZ's and regions, and making sure connectivity exist between those)
* Hardware for global infrastructure (replacing servers, switches, and networking gear)
* Configuration management for infrastructure (how bits of data get from one location to another)
* Patching cloud infrastructure and services (core servers or bare metal servers that are running virtual servers and servers running services used on AWS)

### Customer Responsibility

* Individual access to cloud resources and training (least privilege access to people in our company that need to access cloud resources; train them to use services on AWS)
* Data security and encryption both in transit and at rest (i.e. if you put unencrypted in S3 it is bad; but should encrypt it at rest)
* Operating system, network and firewall configurations (if you are using IaaS; EC2 virtual servers, you are responsible for the OS including patching; if you are configuring your own VPCs, you are responsible for the network configuration, access control lists and security groups)
* All code you deployed onto cloud infrastructure (code you upload)
* Patching guest operating system and custom applications
  * Whereas the host operating system is software installed on a computer to interact with the hardware, the guest operating system is software installed onto and running on the virtual machine

### AWS Well-architected Framework  

* The Well-architected Framework is a collection of best practices across five key pillars for how to best create systems that create business value on AWS

### Pillars of the Well-architected Framework

![image](https://user-images.githubusercontent.com/114364831/214117366-f5bcb0f6-9472-4856-92d8-6126e9c93c99.png)

### High-availability and Fault Tolerance

"Everything fails all the time"

* Fall under the reliability pillar of the Well-architected Framework

### Reliability on AWS

![image](https://user-images.githubusercontent.com/114364831/214119307-64e4da87-0be0-40df-b0f1-5b830bc2d60b.png)

