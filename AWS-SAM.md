### AWS Serverless Application Model (SAM) 

AWS SAM is an open-source framework that can be used to build **serverless applications** on AWS.
  
A **serverless application** is a combination of Lambda functions, event sources, and other resources that work together to perform tasks.
* A serverless application is more than just a Lambda function - it can include additional resources such as APIs, databases, and event source mappings.

AWS SAM can be used to define serverless applications. AWS SAM consists of the following components:

* **AWS SAM template specification**. This specification can be used to define a serverless application. It provides a simple and clean syntax to describe the functions, APIs, permissions, configurations, and events that make up a serverless application. An AWS SAM template file can be used to operate on a single, deployable, versioned entity (a serverless application).

* **AWS SAM command line interface (AWS SAM CLI)**. This tool can be used to build serverless applications that are defined by AWS SAM templates. The CLI provides commands that enable a developer to verify that AWS SAM template files are written according to the specification, invoke Lambda functions locally, step-through debug Lambda functions, package and deploy serverless applications to the AWS Cloud, etc.

### AWS SAM template anatomy

An AWS SAM template file closely follows the format of an AWS CloudFormation template file. The primary differences between AWS SAM template files and AWS CloudFormation template files are the following:

* **Transform declaration**. The declaration Transform: `AWS::Serverless-2016-10-31` is required for AWS SAM template files. This declaration identifies an AWS CloudFormation template file as an AWS SAM template file.
* **Globals section**. The `Globals` section is unique to AWS SAM. It defines **properties that are common to all your serverless functions and APIs**. All the `AWS::Serverless::Function`, `AWS::Serverless::Api`, and `AWS::Serverless::SimpleTable` resources inherit the properties that are defined in the Globals section.
* **Resources section**. In AWS SAM templates the `Resources` section can contain a combination of AWS CloudFormation resources and AWS SAM resources.
* **Parameters section**. Objects that are declared in the `Parameters` section cause the `sam deploy --guided` command to present additional prompts to the user. 
   * These prompts allow the user to customize certain aspects of the application, such as environment variables or resource configurations, before deploying it. Essentially, parameters allow for dynamic input to be provided to the application at runtime.
