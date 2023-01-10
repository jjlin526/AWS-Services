### AWS Serverless Application Model (SAM) 

AWS SAM is an open-source framework that can be used to build **serverless applications** on AWS.
  
A **serverless application** is a combination of Lambda functions, event sources, and other resources that work together to perform tasks.
* A serverless application is more than just a Lambda function - it can include additional resources such as APIs, databases, and event source mappings.

AWS SAM can be used to define serverless applications. AWS SAM consists of the following components:

* **AWS SAM template specification**. This specification can be used to define a serverless application. It provides a simple and clean syntax to describe the functions, APIs, permissions, configurations, and events that make up a serverless application. An AWS SAM template file can be used to operate on a single, deployable, versioned entity (a serverless application).

* **AWS SAM command line interface (AWS SAM CLI)**. This tool can be used to build serverless applications that are defined by AWS SAM templates. The CLI provides commands that enable a developer to verify that AWS SAM template files are written according to the specification, invoke Lambda functions locally, step-through debug Lambda functions, package and deploy serverless applications to the AWS Cloud, etc.
