### Amazon Elastic Compute Cloud (Amazon EC2)

EC2 provides **secure and resizable compute capacity** for virtually any workload
* Instances running computing operations can increase or decrease at will

### Amazon Machine Image (AMI)

* An Amazon Machine Image (AMI) is a supported and maintained image provided by AWS that provides the information required to launch an instance
* An AMI must be specified when an instance is launched
* Multiple instances can be launched from a single AMI if multiple instances with the same configuration are required
* An AMI is composed of an operating system and software used on an EC2 instance
* Amazon updates the image software (but not your instance) -- must either manually make updates or create a new instance and migrate application code for security patches

![image](https://user-images.githubusercontent.com/114364831/211567733-101f8ce3-5f2a-4ac6-a903-8bbf83ad292a.png)

### Basic Unit of EC2

* EC2 instance

### Auto Scaling Group

* Rules for automatically scaling EC2 instances up and down 
* Use EC2 for scaling AMIs
* Use EB for scaling applications

### Elastic Block Store (EBS)

* Storage service that makes it easy to calculate charges for storage
* Volumes that live independently of EC2 instances, and can be retained or deleted when EC2 instance is deleted

### EBS vs S3

* Use EBS for EC2 file systems - used specifically with EC2
* Use S3 for file storage (storing and serving up independent files)

### Steps to Launch an EC2 Instance

1. Choose AMI
2. Choose instance type
3. Configure instance
4. Add storage
5. Tag instance (meta values added to instance)
6. Configure security group
7. Review (create instance with key pair)

### Security Group

* IP-based communication rules for a single or group of EC2 instances
* Little firewalls configured at per-instance basis
* A security group controls which IPs can talk to the instance and which instance the IPs can talk to

### Example Security Group Scenarios

* Control who can SSH into EC2 instance
* Allow access between EC2 instances
* Allow access to databases
* Accept HTTP requests

### Amazon EC2 Pricing

* EC2 instances are charged by the hour based on : instance type and AMI type (Windows image costs more than a Linux image due to licensing paid for by Amazon)

### EC2 Instance Pricing

* Spots instances are cheaper than reserved instances which are cheaper than on-demand instances.
