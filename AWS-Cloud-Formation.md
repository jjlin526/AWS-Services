### AWS CloudFormation

* AWS CloudFormation speeds up **cloud provisioning with infrastructure as code (IaC)**
* AWS CloudFormation is a service that helps you model and set up your AWS resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS 
* You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and CloudFormation takes care of provisioning and configuring those resources for you
* You do not need to individually create and configure AWS resources and figure out what is dependent on what; CloudFormation handles that

### What is Infrastructure as Code (IAC)?

* Infrastructure as Code (IaC) is the managing and provisioning of infrastructure through **code instead of through manual processes**. With IaC, configuration files are created that contain infrastructure specifications, which makes it easier to edit and distribute configurations.

AWS CloudFormation enables a user to model, provision, and manage AWS and third-party resources by treating infrastructure as code.  

![image](https://user-images.githubusercontent.com/114364831/211565355-516b2ef4-55af-4ddf-a655-2d7fcf1f673b.png)

### Scenarios in which CloudFormation can help

#### Simplify infrastructure management
* For a scalable web application that also includes a backend database, you might use an Auto Scaling group, an Elastic Load Balancing load balancer, and an Amazon Relational Database Service database instance. You might use each individual service to provision these resources and after you create the resources, you would have to configure them to work together. All these tasks can add complexity and time before you even get your application up and running.
* Instead, you can create a CloudFormation template or modify an existing one. A template describes all your resources and their properties. When you use that template to create a CloudFormation stack, CloudFormation provisions the Auto Scaling group, load balancer, and database for you. After the stack has been successfully created, your AWS resources are up and running. You can delete the stack just as easily, which deletes all the resources in the stack. By using CloudFormation, you easily manage a collection of resources as a single unit.

#### Quickly replicate your infrastructure
* If your application requires additional availability, you might replicate it in multiple regions so that if one region becomes unavailable, your users can still use your application in other regions. The challenge in replicating your application is that it also requires you to replicate your resources. Not only do you need to record all the resources that your application requires, but you must also provision and configure those resources in each region.
* Reuse your CloudFormation template to create your resources in a consistent and repeatable manner. To reuse your template, describe your resources once and then provision the same resources over and over in multiple regions.
