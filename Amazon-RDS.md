### Amazon RDS

Amazon Relational Database Service (RDS) is a distributed, **cloud-based database platform** that makes it easy to set up, operate, and scale a relational database  

* Seven popular engines — Amazon Aurora with MySQL compatibility, Amazon Aurora with PostgreSQL compatibility, MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server — can be deployed on-premises with Amazon RDS on AWS Outposts

### Managed Database Aspects

* Scheduled automated backups
* Simple software updates
* Managed infrastructure

### Database on EC2 vs. RDS

Installing own database on EC2 instances:
* Database backsup
* Redundancy
* Software patches (i.e. security)

RDS
* AWS handles it all
* Easy configuration
* Read replicas

### RDS Databases Run on EC2 Instances

* Determine type of EC2 instance it will be running on
* Decide what type of performance database will need based on load it will be under

### RDS Makes it Easy to...

* Take DB snapshots
* Change the hardware (i.e. increase size of EC2 instance used to back the database)

### RDS Security

* Access is controlled using Security Groups
* By configuring the Security Group for the instantiated RDS database, the application (i.e. EC2) can be allowed access to the database but block any other connections (external applications)
* Can configure ways for BI tools to connect, so that users can query the databases 

### RDS Pricing Structure

Depends on:
* Type of database
* Region
* EC2 instance type

### Other Managed Database Offerings from Amazon

* DynamoDB (NoSQL database)
* DocumentDB (MongoDB-compatible NoSQL database)

![image](https://user-images.githubusercontent.com/114364831/211411090-2773d9ee-4e73-460c-82e4-ff45ae3ac2e0.png)  



