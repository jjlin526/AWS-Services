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

### Amazon Simple Queue Service (SQS)
* Fully managed message queue service
* Enables you to build decoupled and fault tolerant applications
* Supports up to 256 KB data payload (for a message)
* Allows messages to be stored up to 14 days
* Provides two types of queues:
    * Standard queue (does not guarantee order of items pulled off queue)
    * FIFO queue (first in first out)

### Example Amazon SNS and SQS Architecture

![image](https://user-images.githubusercontent.com/114364831/213790868-b983041b-54c7-4ffe-89c1-db747821b7e7.png)

SNS is a messaging service that allows for decoupling of applications and can be used for notifications, triggering lambdas, sending SMS and Email messages, and fan-out delivery to multiple endpoints. SQS is a message queuing service that enables decoupling of application components and can be used for building distributed applications, sending messages between microservices and storing logs. Analytics Ingestion Service is a service that helps to collect, transform and load data into a centralized data store, it allows for easy ingestion and processing of large volumes of data from various sources into data lake or data warehouse, which can be used for data warehousing or Business Intelligence.
