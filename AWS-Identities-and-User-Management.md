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
