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

### Pilot Light

* Key infrastructure components are kept running in the cloud
* Designed to reduce recovery time over the Backup and Restore approach
* Does incur cost of this infrastructure continually running in the cloud
* AMI's are prepared for additional systems and can be launched quickly

### Definition of Pilot Light  

* The pilot light method gives you a quicker recovery time than the backup-and-restore method because the core pieces of the system are already running and are continually kept up to date.

### Warm Standby

* A scaled-down version of the full environment is running in the cloud
* Critical systems can be running on less capable instance types
* Instance types and other systems can be ramped up for disaster recovery event
* Does incur cost of this infrastructure continually running in the cloud

### Multi Site

* Full environment is running in the cloud at all times
* Utilizes instance types needed for production not just recovery
* Provides a near seamless recovery process
* Incurs the most cost over the other approaches

### Selecting a Disaster Recovery Architecture

### Disaster Recovery Approach Considerations

![image](https://user-images.githubusercontent.com/114364831/214620361-e8ad3fc5-e42f-4f13-806f-3e3e38a95f27.png)

### Recovery Time Objective (RTO)

* The time it takes to get your systems back up and running to the ideal business state after a disaster recovery event

### Recovery Point Objective

* The amount of data loss (in terms of time) for a production system during a disaster recovery event (i.e. RPO of an hour means data loss for an hour)

### Summary

* Understood the need for a disaster recovery strategy
* Reviewed the four different disaster recovery approaches on AWS
* Explored the factors to know when selecting an approach (RTO, RPO -- data)
* Examined specific scenarios and disaster recovery needs

### Scenario Based Review

### Scenario 1

Roger's company runs several production workloads in AWS. Roger is tasked with architecting the disaster recovering approach. His organizations want there to be a seamless transition during an event. Which disaster recovery approach would Roger's company use for this?

* **Multi Site approach** (full production instances running both in own data center and in AWS)

### Scenario 2

Jennifer's company is a startup. They do not currently have a disaster recovery approach. In this case, minimizing cost is more critical than minimizing RTO. What disaster recovery approach would you recommend to Jennifer?

* **Backup and Restore approach** (minimize cost; higher RTO)

### Scenario 3

Eliza is documenting her company's disaster recovery approach. They keep a few key servers up and running in AWS in case of an event. These servers have smaller instance types than what production would need. Which disaster recovery approach most closely matches this scenario?

* **Pilot Light approach** (only a few key servers; core systems up and running in the cloud; have to launch other instances that support their environment if there is a DR event)
