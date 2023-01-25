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

### Network ACL

* Works at the subnet level with a VPC (when you define a network configuration, every server that gets spun up within a subnet will adopt the ACL for that subnet) 
* Enables you to allow and deny traffic
* Each VPC has a default ACL that allows all inbound and outbound traffic
* Custom ACL's deny all traffic until rules are added

### AWS VPN

* Creates an encrypted tunnel into your VPC (may not even want VPC available to public internet; but still want access to manage servers within VPC)
* Can be used to connect your data center or even individual client machines
* Supported in two services:
    * Site-to-site VPN
    * Client VPN

### Site-to-site VPN Example

![image](https://user-images.githubusercontent.com/114364831/214670775-5b5292bb-0b55-4795-8e4b-b15da671280f.png)

* Have servers in data center that must interact with EC2 instances within VPC on AWS
* Can utilize AWS VPN service - create customer gateway and end that info into the service, and then a VPN gateway within VPC on AWS; enables encrypted traffic travelling between corporate data center and AWS
* Direct Connect connects to AWS global infrastructure without using public internet; AWS VPN does use public internet, but is encrypted the entire way

### Protecting Infrastructure from Attacks

### Security Services

![image](https://user-images.githubusercontent.com/114364831/214673448-29760e62-3386-4f22-b15b-440830417251.png)

### Distributed Denial of Service (DDoS)

* A type of attack where a server or group of servers are flooded with more traffic than they can handle in a coordinated effort to bring the system down

### AWS Shield

* Provides protection against DDoS attacks for apps running on AWS
* Enables on-going threat detection and mitigation
* Has two different service levels:
     * Standard
     * Advanced

### AWS Macie

* Utilizes machine learning to analyze data stored in Amazon S3
* It can detect personal information and intellectual property in S3 (without us having to classify the data; prevents leaks through categorization)
* Provides dashboards that show how the data is being stored and accessed
* Enables alerts if it detects anything unusual about data access (anomaly detection using machine learning -- detect strange patterns in data access; detection that we could not do if monitoring manually)

### Amazon Inspector

* Enables scanning of Amazon EC2 instances for security vulnerabilities (keeping instances up to date; patched for critical vulnerabilities; following best practices -- run Inspector in on-demand manner)
* Charged by instance per assessment run (i.e. choose to run assessment on 10 instances - will be charged accordingly)
* Two types of rules packages:
     * Network reachability assessment (understand what is available to the internet from servers)
     * Host assessment (check EC2 instances to make sure they have been patched for critical vulnerabilities and that no common configuration errors have been made within the server)
