### Elastic Beanstalk

* Application service that makes it easy to run code and scale it on AWS
* Running on EC2 instances under the covers

### Deploying Your App to EC2

* Manual configuration
* Manual code deployment
* Restricted command line interface
* Scale with AMIs
* Manual monitoring (i.e. third-party services or custom CloudWatch rules)
  * Elastic Beanstalk handles all the above scenarios automatically

### Deploying Your App with EB

* Easy deployment with various tools
* Set it and forget it configuration
* Aggregated monitoring and logging (even when deployed on multiple EC2 instances)

### Elastic Beanstalk Structure

* Main abstract structure in Elastic Beanstalk is a root level application (unique name)
  * Many application versions inside an application - actual code that will run application
  * This code can be deployed to an environment (i.e. Test Environment, Production Environment)
    * Environment is the rules and configuration that manages actual EC2 instances
    * Each environment can run with a different platform (i.e. Java or Node) and can be configured with certain EC2 instance types (e.g. t2.micro, m4.xlarge)
    * Configuring each environment will require the most time (can set up deployment, load balancing and scaling rules there)
  * Application versions are stored in S3 bucket
  * Each application has a limit of 1000 application versions (delete old, unneeded versions if this limit is hit)

### Elastic Beanstalk Monitoring Dashboard

* Options not as robust as a full monitoring suite
* Data aggregated from all application instances (truly see what application is doing, instead of one single instance)

### Monitoring Metric Examples

* Number of requests
* CPU utilization
* Network traffic

### Elastic Beanstalk Logs Dashboard
* Functionality to easily pull logs from all instances
* No need to log in to each EC2 instance and manually download the logs
* EB is free, only need to pay for EC2 instances, load balancers, and S3 separately
