### AWS CloudFormation

* AWS CloudFormation speeds up **cloud provisioning with infrastructure as code (IaC)**
* AWS CloudFormation is a service that helps you model and set up your AWS resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS 
* You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and CloudFormation takes care of provisioning and configuring those resources for you
* You do not need to individually create and configure AWS resources and figure out what is dependent on what; CloudFormation handles that

* **Infrastructure as Code (IaC)**: CloudFormation enables you to provision, manage and deploy your infrastructure as code, meaning you can describe your infrastructure resources in a text file and version-control that file alongside your other code.

* **Template-Based Deployment**: CloudFormation uses templates, written in JSON or YAML, to define and deploy the required resources in your infrastructure. These templates are declarative and you only need to specify what resources you need, not how to create them.

* **Stack**: A CloudFormation stack is a collection of AWS resources that you can manage as a single unit. You can create, update and delete a stack as a whole, making it easier to manage complex infrastructures. Stacks also provide a way to track changes to your infrastructure and revert to previous versions if necessary.

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

#### Easily control and track changes to your infrastructure
* In some cases, you might have underlying resources that you want to upgrade incrementally. For example, you might change to a higher performing instance type in your Auto Scaling launch configuration so that you can reduce the maximum number of instances in your Auto Scaling group. If problems occur after you complete the update, you might need to roll back your infrastructure to the original settings. To do this manually, you not only have to remember which resources were changed, you also have to know what the original settings were.
* When you provision your infrastructure with CloudFormation, the CloudFormation template describes exactly what resources are provisioned and their settings. Because these templates are text files, you simply track differences in your templates to track changes to your infrastructure, similar to the way developers control revisions to source code. For example, you can use a version control system with your templates so that you know exactly what changes were made, who made them, and when. If at any point you need to reverse changes to your infrastructure, you can use a previous version of your template.

### Template Anatomy

A template is a **JSON- or YAML-formatted text file** that **describes your AWS infrastructure**. The following examples show an AWS CloudFormation template structure and its sections.

### JSON

The following example shows a JSON-formatted template fragment.

```json
{
  "AWSTemplateFormatVersion" : "version date",

  "Description" : "JSON string",

  "Metadata" : {
    template metadata
  },

  "Parameters" : {
    set of parameters
  },
  
  "Rules" : {
    set of rules
  },

  "Mappings" : {
    set of mappings
  },

  "Conditions" : {
    set of conditions
  },

  "Transform" : {
    set of transforms
  },

  "Resources" : {
    set of resources
  },
  
  "Outputs" : {
    set of outputs
  }
}
```

### YAML

The following example shows a YAML-formatted template fragment.

```yaml
AWSTemplateFormatVersion: "version date"

Description:
  String

Metadata:
  template metadata

Parameters:
  set of parameters

Rules:
  set of rules

Mappings:
  set of mappings

Conditions:
  set of conditions

Transform:
  set of transforms

Resources:
  set of resources

Outputs:
  set of outputs
```

### Template sections

Templates include several major sections. The `Resources` section is the only required section. Some sections in a template can be in any order. However, as you build your template, it can be helpful to use the logical order shown in the following list because values in one section might refer to values from a previous section.

* **Format Version** (optional)
The AWS CloudFormation template version that the template conforms to. The template format version isn't the same as the API or WSDL version. The template format version can change independently of the API and WSDL versions.

* **Description** (optional)
A text string that describes the template. This section must always follow the template format version section.

* **Metadata** (optional)
Objects that provide additional information about the template.

* **Parameters** (optional)
Values to pass to your template at runtime (**when you create or update a stack**). You can refer to parameters from the `Resources` and `Outputs` sections of the template.

* **Rules** (optional)
Validates a parameter or a combination of parameters passed to a template during a stack creation or stack update.

* **Mappings** (optional)
A mapping of keys and associated values that you can use to specify conditional parameter values, similar to a lookup table. You can match a key to a corresponding value by using the Fn::FindInMap intrinsic function in the Resources and Outputs sections.

* **Conditions** (optional)
Conditions that control whether certain resources are created or whether certain resource properties are assigned a value during stack creation or update. For example, you could conditionally create a resource that depends on whether the stack is for a production or test environment.

* **Transform** (optional)
For serverless applications (also referred to as Lambda-based applications), specifies the version of the AWS Serverless Application Model (AWS SAM) to use. When you specify a transform, you can use AWS SAM syntax to declare resources in your template. The model defines the syntax that you can use and how it's processed. You can also use AWS::Include transforms to work with template snippets that are stored separately from the main AWS CloudFormation template. You can store your snippet files in an Amazon S3 bucket and then reuse the functions across multiple templates.

* **Resources** (required)
Specifies the stack resources and their properties, such as an Amazon Elastic Compute Cloud instance or an Amazon Simple Storage Service bucket. You can refer to resources in the Resources and Outputs sections of the template.

* **Outputs** (optional)
Describes the values that are returned whenever you view your stack's properties. For example, you can declare an output for an S3 bucket name and then call the `aws cloudformation describe-stacks` AWS CLI command to view the name.
