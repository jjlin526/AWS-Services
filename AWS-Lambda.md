### AWS Lambda

AWS Lambda is a **serverless compute service** that runs code in response to events and automatically manages the underlying compute resources

* These events may include changes in state or an update, such as a user placing an item in a shopping cart on an e-commerce website
* You can use AWS Lambda to extend other AWS services with custom logic, or create your own backend services that operate at AWS scale, performance, and security
* AWS Lambda automatically runs code in response to multiple events, such as HTTP requests via Amazon API Gateway, modifications to objects in Amazon Simple Storage Service (Amazon S3) buckets, table updates in Amazon DynamoDB, and state transitions in AWS Step Functions.
* Lambda runs code on high availability compute infrastructure and performs all the administration of the compute resources. This includes server and operating system maintenance, capacity provisioning and automatic scaling, code and security patch deployment, and code monitoring and logging. All that is required is to supply the code

Use Amazon S3 to trigger AWS Lambda data processing in real time after an upload, or connect to an existing Amazon EFS file system to enable massively parallel shared access for large-scale file processing.  

![image](https://user-images.githubusercontent.com/114364831/211413637-fa80ecfd-5ffe-4818-b503-98f3b80481c6.png)
