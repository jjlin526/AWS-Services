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

### Deploying Pre-defined Solutions on AWS

![image](https://user-images.githubusercontent.com/114364831/214686516-b59c8b7d-bda3-478a-872f-29ccea74d141.png)

### AWS Service Catalog

* Targeted to serve as an organizational service catalog for the cloud
* Can include single server image to multi-tier custom applications (wide variety of infrastructure needs)
* Enables organizations to leverage services that meet compliance (if your IT group has already constructed a specific way to launch a certain type of server and made sure it follows all organizational and industry best practices - others do not have to reinvent the wheel)
* Supports a lifecycle for services released in the catalog (version 1, update it to version 1.1 - everyone using it would be notified that there is an update to the service they are using)

### AWS Marketplace

* Geared at third-party vendors or Independent Software Vendors (ISV) who are going to publish their software for use on AWS
* Curated catalog of third-party solutions for customers to run on AWS
* Provides AMI's, CloudFormation stacks, and SaaS based solutions
* Enables different pricing options to overcome licensing in the cloud (third-party vendors have licensing more tied to physical servers)
* Charges appear on your AWS bill (some things are free and some have charges on top of AWS infrastructure costs)

### Developer Tools

### AWS Developer Services

![image](https://user-images.githubusercontent.com/114364831/214693493-b627b3f2-899e-4d4e-87b1-9590d23f102c.png)

* AWS CodeCommit is a managed source code repository using git; alternative to GitHub; deeply integrated with AWS
* AWS CodeBuild is a build service (continuous integration); run build commands for custom apps to create output artifacts
* AWS CodeDeploy takes care of deployment out to many AWS services
* AWS CodePipeline knows how to work with all other services mentioned previously to create a pipeline; enables us to look at whole process of building, testing and deploying apps
* AWS CodeStar bootstraps entire process for custom apps

### AWS CodeCommit

* Managed source control service
* Utilizes Git for repositories
* Controls access with IAM policies (control access to this just like any other AWS resource)
* Serves as an alternative to Github and Bitbucket

### AWS CodeBuild

* Fully managed build and continuous integration service on AWS
* Do not have to worry about maintaining infrastructure
* Charged per minute for compute resources you utilize
     * Builds application and creates output artifacts

### AWS CodeDeploy

* Managed deployment service for deploying your custom applications
* Deploys to Amazon EC2, AWS Fargate, AWS Lambda, and on-premise servers
* Provides dashboard for deployments in the AWS console (track deployments or start new deployments from console)

### AWS CodePipeline

* Fully-managed continuous delivery service on AWS
* Provides the capabilities to automate building, testing, and deploying (integrate with previous services; can work with source code in CodeCommit; can then build and test within CodeBuild; and use CodeDeploy to deploy output artifacts)
* Integrates with other developer tools as well as Github

### AWS CodeStar

* Workflow tool that automates the use of the other developer services
* Creates a complete continuous delivery toolchain for a custom application
* Provides custom dashboards and configurations in the AWS Console (how all pieces work together)
* You only are charged for the other services you leverage (do not pay for service; just a tool that makes it easier to work with other AWS services)

### Summary

* Reviewed scaling approaches and services for Amazon EC2 (horizontal/vertical scaling, auto scaling, ELBs)
* Examined approaches for controlling access to Amazon EC2 instances (security groups, network ACLs, AWS VPN)
* Explored services to protect infrastructure from hacking and attacks (Shield, Macie, Inspector)
* Introduced developer tools on AWS (CodeCommit, CodeBuild, CodeDeploy, CodePipeline, CodeStar)
* Reviewed approaches for launching pre-defined solutions on Amazon EC2 (AWS Service Catalog, AWS Marketplace)

### Scaling, Auto Scaling, and ELBs

* Scaling refers to the process of increasing or decreasing the number of resources (such as servers) that a system uses to handle its workload.
* Horizontal scaling involves adding more resources to handle increased workloads, while vertical scaling involves increasing the capacity of existing resources.
* Auto Scaling is a service that automatically adjusts the number of resources used by a system based on the workload, allowing it to scale up or down as needed.
* ELBs (Elastic Load Balancers) are used to distribute incoming traffic across multiple resources, helping to ensure that the workload is distributed evenly and that the system can handle increased traffic.

### Security Groups, Network ACLs, and AWS VPN

* Security Groups are used to control access to resources within a virtual private cloud (VPC) by specifying which incoming and outgoing traffic is allowed (EC2 instance level)
* Network ACLs (Access Control Lists) are another way to control access to resources within a VPC, but at the subnet level.
* AWS VPN (Virtual Private Network) allows you to create a secure connection between your on-premises network and a VPC, allowing you to access resources in the VPC as if they were on your local network.

### Scenario Based Review

* Service Catalog
* Inspector
* 
