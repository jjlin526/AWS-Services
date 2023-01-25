### Architecting Applications on Amazon EC2

### Overview

* Review scaling approaches and services for Amazon EC2
* Examine approaches for controlling access to EC2 instances
* Explore services to protect infrastructure from hacking and attacks
* Introduce developer tools on AWS
* Review approaches for launching pre-defined solutions on Amazon EC2 

### Scaling EC2 Infrastructure

### Scaling on Amazon EC2

![image](https://user-images.githubusercontent.com/114364831/214639682-2e403f7f-24c4-44de-9515-0900ad898667.png)

* Horizontal scaling is a much more sustainable approach than vertical scaling

### Amazon EC2 Horizontal Scaling Services

![image](https://user-images.githubusercontent.com/114364831/214640342-d797c194-beee-42ea-9286-86598c84eb6b.png)

### Amazon EC2 Auto Scaling Group

* Launch template defines the instance configuration for the group (i.e. Windows 2019 server running on a certain instance type and certain security group associated with it -- can be defined in launch template)
* Defines the minimum, maximum, and desired number of instances
* Performs health checks on each instance (i.e. custom health check -- can provide a URL that returns a status code)
* Exists within 1 or more availability zones in a single region (adds a level of fault tolerance)
* Works with on-demand and spot instances

### Amazon EC2 Horizontal Scaling Example

![image](https://user-images.githubusercontent.com/114364831/214645848-fcfdfa74-9119-4f20-be3e-982540d7e7dc.png)

* Application Load Balancer (type of ELB) works with Auto Scaling Group to know which instances are healthy and which are not; routes user traffic based on health

### AWS Secrets Manager

* Secure way to integrate credentials, API keys, tokens, and other secret content (in a way that cannot be compromised; when scaling out to multiple servers)
* Integrates natively with RDS, DocumentDB, and Redshift
* Can auto-rotate credentials with integrated services
* Enables fine-grained access control to secrets

### Controlling Access to EC2 Instances

### Security in Amazon VPC

![image](https://user-images.githubusercontent.com/114364831/214650388-381ed90a-7b25-426c-ab87-2de122acb955.png)

### Security Groups

* Serve as a firewall for your EC2 instances
* Control inbound and outbound traffic
* Works at the instance level (do not work at the subnet or VPC-level, they work at the instance level)
* EC2 instances can belong to multiple security groups (may create security groups for common purposes; i.e. configurations for web servers)
* VPC's have default security groups
* Must be explicitly associated with an EC2 instance
* By default all outbound traffic is allowed (server can send any information out to the internet)
