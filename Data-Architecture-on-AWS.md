### Data Architecture on AWS

### Overview

* Review approaches for integrating data from your own data center
* Examine approaches for processing data
* Explore data analysis approaches
* Integrate machine learning and AI into data analysis

### Integrate On-premise Data

### On-premise Data Integration Services

![image](https://user-images.githubusercontent.com/114364831/214373198-c96c0947-9d2b-43d6-abfb-d2ea442129b7.png)

### AWS Storage Gateway

* Integrates cloud storage into your local network
* Deployed as a VM or specific hardware appliance (running Storage Gateway software onto your network)
* Integrates with S3 and EBS
* Supports three different gateway types:
    * Tape Gateway
    * Volume Gateway
    * File Gateway

* AWS Storage Gateway is a service offered by Amazon Web Services (AWS) that enables on-premises applications to store and retrieve data from AWS storage services, such as Amazon S3 and Amazon Glacier. It provides a seamless integration between on-premises storage infrastructure and the cloud, allowing customers to use the cost and scalability benefits of the cloud while still maintaining control and access to their data on-premises. This service can be used in various scenarios such as backup and archive, disaster recovery, and file sharing.

### Gateway Types

![image](https://user-images.githubusercontent.com/114364831/214376186-952470fc-bf1c-4b25-a0fd-7aed3ab632c7.png)

* **File Gateway**: This type of gateway allows you to store files in Amazon S3 and access them quickly and easily as if they were stored on your own network. It provides a local cache, so the files are stored on S3 but can be accessed with low latency as if they were on your local network.

* **Tape Gateway**: This type of gateway allows you to use the cloud to store your tape backups. It creates virtual tapes in the cloud and uses them as the target for your tape backup processes, so you can store your data in the cloud instead of on physical tapes.

* **Volume Gateway**: This type of gateway allows you to create cloud-based storage volumes that can be accessed by your local applications using iSCSI protocol. It allows you to store data in the cloud and access it as if it were on your own network, using the same tools and workflows you use for local storage.

### AWS DataSync

* Leverages the DataSync agent deployed as a VM on your network
* Integrates with S3, EFS, and FSx for Windows File Server on AWS
* Greatly improved speed of transfer due to custom protocol and optimizations
* Charged per GB of data transferred

### Processing Data

### Data Processing Services

![image](https://user-images.githubusercontent.com/114364831/214418221-ba7f21cc-3c86-4c76-b2b7-ff9e4a2182ec.png)

### AWS Glue

* Fully managed ETL (extract, transform and load) service on AWS
* Supports data in Amazon RDS, DynamoDB, Redshift, and S3
* Supports a serverless model of execution (handles management of infrastructure for you)

### Amazon EMR

* Enables big-data processing on Amazon EC2 and S3
* Supports popular open-source frameworks and tools
* Operates in a clustered environment without additional configuration (on your own in Amazon EC2, lot of config to set up tools and operate in environments with more than one server that must work together)
* Supports many different big-data use cases (supports many tools and has a clustered environment)
