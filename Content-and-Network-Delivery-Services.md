### Content and Network Delivery Services

![image](https://user-images.githubusercontent.com/114364831/212402391-a5015ac3-6aad-46dd-9f7a-ea519cdafc9f.png)

### Amazon VPC and Direct Connect

### Amazon Virtual Private Cloud (VPC)

* A logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define.
* Enables virtual networks in AWS
* Supports IPv4 and IPV6 (different standard for addresses of computers on networks)
* Allows for configuration of:
  * IP address range
  * Subnets
  * Route tables
  * Network gateways

* **Route tables**: A route table contains a set of rules, called routes, that are used to determine where network traffic is directed. Each VPC has a default route table, and you can create additional route tables as needed.

* **Network gateways**: A network gateway is a VPC component that allows communication between your VPC and the Internet or other AWS services. There are two types of network gateways: Internet Gateways and Virtual Private Gateway.

* **Subnets**: A subnet is a range of IP addresses in a VPC. You can launch Amazon Elastic Compute Cloud (EC2) instances in a subnet. You can also associate security groups and network ACLs with a subnet to control inbound and outbound traffic.

* **Security groups**: A security group acts as a virtual firewall for your instance to control inbound and outbound traffic.

* **Network ACLs**: A network ACL is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.

* Supports public and private subnets
* Can utilize **NAT** for private subnets
  * In Amazon VPC, a NAT device is a virtual machine (VM) that sits in a public subnet and acts as a gateway for instances in a private subnet. Instances in the private subnet send their outbound traffic to the NAT device, which then forwards it to the Internet. The NAT device also translates the private IP addresses of the instances in the private subnet to the public IP address assigned to the NAT device, allowing the Internet to respond to the requests.
* Enables a connection to your data center
* Can connect to other VPC's (peering connection)
* Supports private connections to many AWS services
  * Sensitive applications can stay within VPC (does not have to send traffic through internet) even when using specific AWS services

### AWS Direct Connect

* A cloud service solution that makes it easy to establish a dedicated netowrk connection from your data center to AWS (or a VPC)
* E.g. you have a business app that uses app data stored in data center, but app itself runs on AWS. It would be ideal to have a high-speed connection between your data center and app directly, without having to send it through the internet
