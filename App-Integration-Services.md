### App Integration Services

![image](https://user-images.githubusercontent.com/114364831/213784049-bb20ebc4-00b8-4801-85b6-9e77230accdd.png)

### Overview

* Introducing Amazon Simple Notification Service (SNS)
* Introducing Amazon Simple Queue Service (SQS)
* Exploring architectures leveraging SNS and SQS
* Examining AWS Step Functions
* Reviewing sample AWS Step Function usage

### AWS Messaging Services

### Amazon Simple Notification Service (SNS)

* Fully managed pub/sub messaging service (publish/subscribe -- i.e. public messages about new orders and subscribe to new orders or order refunds, etc.)
* Enables you to create decoupled applications 
* Organized according to topics
* Integrates with multiple AWS services
* Provides end user notifications across SMS, email, and push notifications

### Example Amazon SNS Architecture (for a SaaS company)

![image](https://user-images.githubusercontent.com/114364831/213788328-4a8ff274-9ba9-44f0-83df-238740a5fba8.png)

