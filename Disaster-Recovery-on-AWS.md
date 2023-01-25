### Disaster Recovery on AWS

* Disaster recovery (DR) is about preparing for and recovering from a disaster. Any event that has a negative impact on a company's business continuity or finances could be termed a disaster. This includes hardware or software failure, a network outage, a power outage, physical damage to a building like fire or flooding, human error, or some other significant event.

### Needs for Disaster Recovery

* Data center
* Cloud deployment

### Overview

* Understand the need for disaster recovery strategy
* Review the four different disaster recovery approaches on AWS
* Explore the factors to know when selecting an approach
* Examine specific scenarios and disaster recovery needs

### Disaster Recovery Architectures

### Disaster Recovery Scenarios

![image](https://user-images.githubusercontent.com/114364831/214601099-4daf5d08-d767-4154-9de2-6f9ad66b8d21.png)

### Backup and Restore

* Production data is backed up into Amazon S3
* Data can be stored in either standard or archival storage classes
* EBS data can be stored as snapshots in Amazon S3 also
* In a Disaster Recovery event, a process is started to launch a new environment (completely new environment; spin up all servers and database instances)
* This approach has the longest recovery time (least cost)
