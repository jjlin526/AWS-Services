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
