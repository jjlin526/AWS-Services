### Management and Governance Services

![image](https://user-images.githubusercontent.com/114364831/214060077-aa1cc7e0-dd97-4a33-89d5-47dcf4240255.png)

### Overview

* Reviewing the ecosystem of services that are provided for management (after resources have been launched to the cloud)
* Examining how to create an audit trail with AWS CloudTrail
* Exploring how you track infrastructure with CloudWatch and Config
* Introducing infrastructure automation with CloudFormation
* Looking at operational insights with Systems Manager
* Reviewing AWS Organizations leveraging Control Tower

### AWS CloudTrail

* With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services.

### More on CloudTrail

* Inserts audit trail in an S3 bucket or into CloudWatch Logs
* Logs events in the regions in which they occur
* Meets many compliance requirements for infrastructure auditing
* As a best practice, it should be enabled on every AWS account
* Can be consolidated into an Organizational trail using AWS Organizations

### AWS CloudTrail Use Cases

* Compliance requirement
* Forensic analysis (data breach -- what actions were taken against infrastructure)
* Operational analysis (who potentially changed infrastructure that caused a crash or outage)
* Troubleshooting (when a specific bad configuration was injected into the system and use that to fix any issues within infrastructure)

### Managing Infrastructure

![image](https://user-images.githubusercontent.com/114364831/214063539-b01614ed-bb49-45b7-b21e-1f942d9c9811.png)

* Monitoring and management service
* Collects logs, metrics, and events from most AWS services (metric -- i.e. number of users visiting a load balancer; first class citizen: most AWS services integrate with CloudWatch by default)
* Enables alarms based on metrics (CloudWatch will let you know if something is down or not performing as it should; do not need to find it yourself or have customers tell you)
* Provides visualization capabilities for metrics (chart of metric over time)
* Allows for custom dashboards based on collected metrics

### Sample CloudWatch Dashboard

![image](https://user-images.githubusercontent.com/114364831/214068630-472030f3-6c6f-442a-a6cd-c0b0562cbd7f.png)

* CPU utilization on EC2 server, network traffic, EBS activity

### AWS Config Definition

* AWS Config continuously monitors and records your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations

### AWS Config

* Provides configuration history for infrastructure
* Works against rules that you can customize or even create your own custom validations
* Includes conformance packs for compliance standards including PCI-DSS
* Can work with AWS Organizations for both cross-region and cross-account setup
* Provides remediation steps for infrastructure not meeting criteria

### AWS Systems Manager

* AWS Systems Manager provides a unified user interface so you can view operational data from multiple AWS services and allows you to automate operational tasks across your AWS resources

### Overview of Systems Manager

* Provides multiple tools that make it easier to manage your AWS infrastructure
* Enables automation tasks for common maintenance actions (two apps in AWS account, 10 servers that support one app and 10 servers that support another; want to update EC2 instances for first app with new version of a library; can write action one time and send it out to all servers that need to receive it; can choose to have it update on those servers but not on the other servers)
* Gives a secure way to access servers using only AWS credentials (do not have to deal with separate keys or passwords)
* Stores commonly used parameters securely for operational use (have database password and do not want to store that with each app, but want each app to have access to the password when they launch -- can use Systems Manager)

### AWS CloudFormation

* Custom app requires 2 S3 buckets, 5 EC2 servers, 2 SQS queues and 3 lambda functions... could set it up all in the console. Lot of manual steps - what happens if we miss one or incorrectly apply settings to a resource? CloudFormation exists to solve this problem

### Overview of AWS CloudFormation

* Managed service for provisioning infrastructure based on templates (no need to manually clicking in console or writing custom CLI script or using SDK to write custom logic for creating infrastructure)
* No additional charge (only pay for resources launched, service itself has no charge)
* Templates can be YAML or JSON
* Enables infrastructure as code (write a template that every resource on team can use to launch infrastructure -- remove manual processes)
* Manages dependencies between resources (i.e. require one resource to be in place before launching another one; these dependencies are managed)
* Provides drift detection to find changes in your infrastructure (i.e. someone changes S3 permission to be globally available; change will be noticed)

### Example CloudFormation YAML

* The code above if placed within a full CloudFormation template would create a single S3 bucket

![image](https://user-images.githubusercontent.com/114364831/214078335-3bc157d6-6df2-498e-bed7-4e39677d704e.png)

* Can have an environment for testing and one for production and ensure both are the same because of template using CloudFormation

### AWS OpsWorks

* Configuration management service
* Provides managed instances of Chef and Puppet
    * Chef and Puppet are automation platforms that allow you to use code to automate the configurations of your servers
* Configuration is defined as code for servers
* Chef and Puppet manage the lifecycle of these configuration changes with servers
* Works in a hybrid cloud architecture for both cloud-based and on-premise servers

### AWS OpsWorks Services

### AWS OpsWorks Services

![image](https://user-images.githubusercontent.com/114364831/214081062-e34d1810-02f5-4c67-b69c-5f95bbba7dc0.png)

* OpsWorks Stack allows you to define app in layers and manage that using Chef Recipes with Chef Solo

### AWS Organizations

* Allows organizations to manage multiple accounts under a single master account
* Provides organizations with the ability to leverage Consolidated Billing for all accounts
* Enables organizations to centralize logging and security standards across accounts

AWS collected the best practices for multi-account setup under a service called **Control Tower**.

### AWS Control Tower

* A service to create a multi-account environment on AWS that follows the recommended best practices in operational efficiency, security and governance
     * AWS Control Tower creates an abstraction or orchestration layer that combines and integrates the capabilities of several other AWS services, including AWS Organizations, AWS Single Sign-on, and AWS Service Catalog.

### AWS Control Tower

* Centralizes users across all AWS accounts (minimizes effort needed to create users across multiple accounts)
* Provides a way to create new AWS accounts based on templates (ensure every AWS account that is created within finance department has specific settings)
* Integrates GuardRails for accounts (protection for accounts under master account; ensure CloudTrail does not get turned off in any child account -- example GuardRail that can be included)
* Includes a dashboard to gain operational insights from a single view (across all accounts)
