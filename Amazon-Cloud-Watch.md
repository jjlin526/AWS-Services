### Amazon-Cloud Watch

Enables the observation and monitoring of resources and applications on AWS, on premises, and on other clouds.
* Amazon CloudWatch collects and visualizes real-time logs, metrics, and event data in automated dashboards to streamline your infrastructure and application maintenance

### CloudWatch Key Functionality

* Monitoring resources and acting on alerts

### CloudWatch Alarms

* Set up alarms for a multitude of metrics for different AWS services
* For each alarm, choose from a pre-existing set of metrics for each service and set a threshold and actions to take    
  Metric examples:
    * EC2 - CPUUtilization
    * DynamoDB - ConsumedReadCapacityUnits
    * S3 - NumberOfObjects
    * Route53 - HealthCheckStatus
    * RedShift - DatabaseConnections
* Actions include: SMS notification or autoscale EC2 instances, etc.

CloudWatch can monitor and aggregate logs
* Install and configure an awslogs agent on EC2 instances and tell it which logs to send to CloudWatch
* CloudWatch can be configured to filter the logs and send alerts based on criteria defined by the client (i.e. number of times a certain exception occurs in the logs and send a notification once it has occurred a set number of times)

![image](https://user-images.githubusercontent.com/114364831/211656188-f06f8772-e669-4b48-8742-89d5de1a4bf8.png)

![image](https://user-images.githubusercontent.com/114364831/211434702-96ddb048-ad88-4953-aab3-917033ffc098.png)



