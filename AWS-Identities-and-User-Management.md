### AWS Identities and User Management

### Least Privilege Access

* When granting permissions for a user to access AWS resources, you should grant them the minimum permissions needed to complete their tasks and no more.

### Overview

* Introducing AWS Identity and Access Management (IAM)
* Reviewing the IAM identity types
* Enabling Multi-factor Authentication (MFA)
* Introducing Amazon Cognito

### Introduction to AWS IAM

### AWS Identity and Access Management (IAM)

* Service that controls access to AWS resources
* Using the service is free (for everyone who has an AWS account)
* Manages both authentication (what verifies users for us, enables them to login and manage credentials) and authorization (what the user can do; can access all actions on EC2 instances)
* Supports identity federation (use external identity provider to handle authentication of IAM) through Security Assertion Markup Language (SAML) providers including Active Directory
    * Security Assertion Markup Language (SAML) is an XML-based standard for exchanging authentication and authorization data between parties, typically between an identity provider (IdP) and a service provider (SP). SAML allows users to authenticate with one system (such as an Active Directory domain) and then gain access to resources in another system (such as a cloud-based application) without having to re-enter their credentials.
    * Active Directory (AD) is a directory service developed by Microsoft for Windows domain networks. It provides authentication and authorization mechanisms as well as a framework for organizing, securing, and managing network resources. Active Directory is essentially a centralized database that stores information about network resources, including user identities and their associated credentials. It can also be used as an identity provider (IdP) for SAML-based authentication and authorization.
       * So in summary when the IAM system supports identity federation through SAML providers including Active Directory it means that users will be able to use their existing Active Directory credentials to authenticate and gain access to resources controlled by the IAM system.

### AWS IAM Identities

![image](https://user-images.githubusercontent.com/114364831/214150754-82d6dff7-8ba3-4941-99de-bb7fe5fdfd15.png)

* Roles; when you launch an EC2 server, there is an option to specify a role for that server such as access to an S3 bucket (part of web app on that server needs to upload photos to an S3 bucket) -- cannot do this by default, but can give the EC2 server a role with the permission to write to the S3 bucket

### Policies in AWS IAM

![image](https://user-images.githubusercontent.com/114364831/214152148-cc913f6a-d5b1-48dc-b8b2-5256d1648876.png)

* Note that an IAM identity is just a user, group or role

### Example Policy written as JSON Object

![image](https://user-images.githubusercontent.com/114364831/214152751-77a94911-1ee2-4a04-9520-72377c50697b.png)

### AWS IAM Best Practices

![image](https://user-images.githubusercontent.com/114364831/214152975-b0c4ffd9-e45a-4a63-9179-2eee720b6e85.png)

### Demo 1

* Create an IAM user
* Configure permissions for IAM users
* Create an IAM group
* Attach permissions to an IAM group

### Demo 2

* Enable MFA for the root user
* Enable MFA for the IAM user

### Amazon Cognito   

* A managed service that enables you to handle authentication and aspects of authorization for your custom web and mobile applications through AWS.

### Overview of Amazon Cognito

* User directory service for custom applications
* Provides UI components for many platforms
* Provides security capabilities to control account access
* Enables controlled access to AWS resources (can configure access to specific pieces of AWS infrastructure that you would want a user to have access to without signing up for an IAM account)'
* Can work with social and enterprise identity providers

### Amazon Cognito Identity Providers

![image](https://user-images.githubusercontent.com/114364831/214318166-d8a00bb1-83b0-4917-9dd3-1156afe239cb.png)

* Let users login to custom app with Google and have that correspond to a Cognito identity

### Summary

* Introduced AWS Identity and Access Management (IAM)
* Reviewed the IAM identity types (users, groups, roles)
* Enabled Multi-Factor Authentication (MFA)
* Introduced Amazon Cognito

### Scenario-based Review

### Scenario 1

Sylvia manages a team of DevOps engineers for her company. Each member of her team needs to have the same access to cloud systems. It is taking her a long time to attach permissions to each user for access. What approach would help Sylvia manage the team's permissions?

* **Use an IAM Group for the team** (one location for setting permissions for every member of the team -- ensure least privilege access)

### Scenario 2

Edward works for a startup that is building a mapping visualization tool. Their EC2 servers need to access data stored within S3 buckets. Edward created a user in IAM for these servers and uploaded keys (access key and secret access key) to the server. Is Edward following best practices for this approach? If not, what should he do?

* **Use an IAM Role with EC2** (roles are used to give services the permissions to work with other services in AWS in a secure way)

### Scenario 3

William is leading the effort to transition his organization to the cloud. His CIO is concerned about securing access to AWS with a password. He asks William to research approaches for additional security. What approach would you recommend to William for this additional security?

* **Use Multi-factor Authentication** (built into AWS; relatively easy to implement; requires other token to login)
