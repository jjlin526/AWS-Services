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
