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

### Amazon Elastic MapReduce (EMR)

* Enables big-data processing on Amazon EC2 and S3
* Supports popular open-source frameworks and tools
* Operates in a clustered environment without additional configuration (on your own in Amazon EC2, lot of config to set up tools and operate in environments with more than one server that must work together)
* Supports many different big-data use cases (supports many tools and has a clustered environment)

### Supported Amazon EMR Frameworks

![image](https://user-images.githubusercontent.com/114364831/214430486-8d3878ef-e180-4dea-8dcb-c67f165441b5.png)

### AWS Data Pipeline

* Managed ETL (extract, transform, and load) service on AWS
* Manages data workflow through AWS services
* Supports S3, EMR, Redshift, DynamoDB, and RDS
* Can integrate on-premise data stores

### Analyzing Data

### Data Analysis Services

![image](https://user-images.githubusercontent.com/114364831/214462986-185a2c85-adca-4150-955b-feaec7cc1023.png)

### Amazon Athena

* Fully-managed serverless service
* Enables querying of **large-scale data** stored within **Amazon S3** (i.e. sales year after year)
* Queries are written using standard SQL
* Charged based on data scanned for query (amount of data that must be searched through)

### Amazon Quicksight

* Fully managed business intelligence (BI) service
* Enables dynamic data dashboard based on data stored in AWS
* Charged on a per-user and per-session pricing model (how many authors vs. how many people reading data)
* Multiple versions provided based on needs (standard version vs. enterprise version with different capabilities and cost points)

![image](https://user-images.githubusercontent.com/114364831/214464687-521fc838-5ce6-4a0f-b3e4-3f90cb3d2e62.png)

### Amazon CloudSearch

* Fully-managed search service on AWS
* Support scaling of search infrastructure to meet demand
* Charged per hour and instance type of search infrastructure
* Enables developers to integrate search into custom applications (search through a ton of PDF documents that organization has stored)

### Integrating AI and Machine Learning

### AI and Machine Learning Services

![image](https://user-images.githubusercontent.com/114364831/214465885-57fb11a3-7d5f-4f0e-b4da-7784ad37e05f.png)

### Amazon Rekognition

* Fully-managed image and video recognition deep learning service
* Identifies objects in images
* Identifies objects and actions in videos
* Can detect specific people using facial analysis
* Supports custom labels for your business objects

### Amazon Translate

* Fully-managed service for translation of text
* Currently supports 54 languages
* Can perform language identification
* Works both in batch and real-time (get translation back as we are streaming it in)

### Amazon Transcribe

* Fully-managed speech recognition services
* Recorded speech is converted into text in custom applications
* Includes a specific sub-service for medical use (transcribe information that has medical terms in it)
* Supports batch and real-time transcription
* Currently supports 31 languages

### Summary

* Reviewed approaches for integrating data from your own data center
* Examined approaches for processing data (i.e. ETL and services that can support it)
* Explored data analysis approaches (i.e. Athena, looking at data in S3, BI dashboards with QuickSight, and custom search solution using CloudSearch)
* Integrated machine learning and AI into data analysis (i.e. Translate, Transcribe, video and iamge analysis with Rekognition)

### Scenario Based Review

### Scenario 1

Ruth is a data scientist for a financial services company. Large-scale data set needs to be processed before analysis. Ruth does not want to manage servers but just wants to define processing. What service would you recommend to Ruth?

* **AWS Glue** (ETL capability in a serverless way)

### Scenario 2

Jessi is a member of the IT team for a biotech company. She is currently working to identify an approach for controlled lab access. She wants to leverage AI to determine access based on facial imaging. Is there an AWS service that can help with this approach?

* **Amazon Rekognition** (store images of specific people and detect those in other images; could integrate that into the camera used for lab access)

### Scenario 3

Roger's company sells custom services around machine learning. His head of sales is trying to find a great way to visualize their sales data. This data is currently stored in Redshift as their data warehouse. What AWS service would allow this access to the data by non-technical resources?

* **Amazon QuickSight** (without querying data; self-service dashboards based on data stored in RedShift)

