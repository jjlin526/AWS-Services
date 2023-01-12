### AWS Global Infrastructure

### AWS Regions 

* Each region is in a specific geographic location
* Each geographic location has a cluster of data centers

![image](https://user-images.githubusercontent.com/114364831/212110707-f28ffb64-dc36-4a66-a89c-e625bb4b41e9.png)

### Availability Zones

* Consists of one or more data centers
* Multiple availability zones are included with each AWS Region
* Located within the geographic area of the AWS Region
* Redundant power, networking and connectivity

### Availability

* Extent to which an application is fulfilling its intended business purpose. Applications that are highly-available are built in a manner where a single failure will not lessen the application's ability to be fully operational.

### Region and Availability Zone Naming

![image](https://user-images.githubusercontent.com/114364831/212119766-18cf8811-6e01-4398-bd3d-2efad450020a.png)

### Local Zones

* AWS Local Zones place computer, storage, database, and other select AWS services closer to end-users. Each AWS Local Zone location is an extension of an AWS Region. AWS Local Zones provide a high-bandwidth, secure connection between local workloads and those running in the AWS Region, allowing you to seamlessly connect to the full range of in-region services through the same API and tool sets.

![image](https://user-images.githubusercontent.com/114364831/212120924-7173ea43-f1ea-4b3e-ae66-bfa7a0cc0a54.png)

### Wavelength Zones

Wavelength Zones are AWS infrastructure deployments that embed AWS compute and storage services within communications service providers' (CSP) 5G networks, so application traffic from 5G devices reach application servers running in Wavelength Zones without leaving the telecommunications network.

### Points of Presence

Points of presence are elements of the AWS global infrastructure that exist outside of AWS regions. These elements are located in or near populated areas, and specific AWS services use them to deliver content to end users as quickly as possible. Within the overall points of presence, there are two types of infrastructure:
* Edge locations
* Regional edge caches

### AWS Edge Locations

* Used as nodes of a global **content delivery network (CDN)**
* Utilized by Amazon CloudFront and Amazon Route 53
* Located globally at over 400 different locations
* Allows AWS to serve content from locations closest to users

### Visualizing AWS Global Infrastructure

* https://aws.amazon.com/about-aws/global-infrastructure/

### Scenarios

1. Jane's company is looking to transition to AWS. They are starting with a few workloads. It is a requirement to store backup data in multiple geographic areas. Which element of the AWS global infrastructure will best suit this need?

* **AWS Region** (deploy workload in one region, but store backup data in other regions)

2. Tim's company serves content through their site to users around the globe. They are looking to optimize performnace to users around the world. They want to leverage a Content Delivery Network (CDN). Which element of the AWS global infrastructure will be used in this case?

* **AWS Edge Location** (utilized by CloudFront)

3. Ellen's company is transitioning one of their legacy applications to AWS. This application requires uptime of at least 99.5%. They want to be sure any issues at a single data center do not cause an outage. Which element of the AWS global infrastructure supports this need?

* **AWS Availability Zone (AZ)** (high uptime requires high availability - taking advantage of multiple AZs within a single region)
