### Amazon Virtual Private Cloud (VPC)

* VPC enables AWS resources to be defined and launched in a **logically isolated virtual network**
* Amazon VPC gives you control over the virtual networking environment, including resource placement, connectivity, and security
* The VPC can be set up in the AWS service console
* Resources can be added to it (i.e. EC2 and RDS instances)
* Finally VPC communication with each other across accounts, Availability Zones, or AWS Regions should be defined

### Virtual Private Cloud Features

* Configure VPC routing tables
* Use NAT Gateways for outbound traffic  

  Use cases:
  * When resources are running in private subnets and a client would like them to have internet connectivity (without assigning public IP addresses to them)
  * When a client wants to connect to AWS services (other than S3) from their private subnet instances that do not have public IPs
  * When a client wants increase the security of a VPC by keeping instances in private subnet and allowing only specific outbound traffic
* Internal IP address allocation

VPCs can communicate with each other across accounts, Availability Zones, and AWS Regions. This diagram shows one possible configuration where, within Region 1, network traffic is shared between a VPC in availability zone 1 and a VPC in availability zone 2. The same architecture is shown for Region 2. The VPCs in Regions 1 and 2 are not able to connect to one another in this example.  

![image](https://user-images.githubusercontent.com/114364831/211413178-96a44737-8f6a-40ae-97f8-ea6e65b0f692.png)

