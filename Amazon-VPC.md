### Amazon Virtual Private Cloud (VPC)

* VPC enables AWS resources to be defined and launched in a **logically isolated virtual network**
* Amazon VPC gives you control over the virtual networking environment, including resource placement, connectivity, and security
* The VPC can be set up in the AWS service console
* Resources can be added to it (i.e. EC2 and RDS instances)
* Finally VPC communication with each other across accounts, Availability Zones, or AWS Regions should be defined

VPCs can communicate with each other across accounts, Availability Zones, and AWS Regions. This diagram shows one possible configuration where, within Region 1, network traffic is shared between a VPC in availability zone 1 and a VPC in availability zone 2. The same architecture is shown for Region 2. The VPCs in Regions 1 and 2 are not able to connect to one another in this example.  

![image](https://user-images.githubusercontent.com/114364831/211413178-96a44737-8f6a-40ae-97f8-ea6e65b0f692.png)
