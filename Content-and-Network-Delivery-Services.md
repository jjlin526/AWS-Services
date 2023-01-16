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

### Amazon Route 53 (DNS Service)

* Domain name service (DNS)
* Global AWS service (not regional -- all changes applied globally)
* Highly available (and enables creation of highly available services)
* Enables global resource routing
   * Send people to specific server based on which country they are coming in from
   * Or, send them to server that responds the fastest

### DNS

* DNS translates more readily memorized domain names to the numerical IP addresses needed for locating and identifying computer services and devices with the underlying network protocols

### Route 53 High Availability

![image](https://user-images.githubusercontent.com/114364831/212410761-152287ce-8e7f-402a-b9ec-718ba1213136.png)

- If us-east-1 server goes down due to deploying a bad configuration, Route 53 can be configured with a failover by routing users to eu-west-1 in Dublin
- User will not know that anything has changed by routing to a new server

### Elastic Load Balancing

### Elasticity

* The ability for the infrastructure supporting an application to grow and contract based on how much it is used at a point in time

### Elastic Load Balancing

* Distributes traffic across multiple targets
* Integrates with EC2, ECS, and Lambda
* Supports one or more AZ's in a region
  * E.g. want to have customer website running across 3 AZ's, want servers in each AZ; leverage ELB to distribute users to the server in one of the three AZ's
* Three types of load balancers:
  * Application Load Balancer (ALB)
  * Network Load Balancer (NLB)
  * Classic Load Balancer (ELB)

### Scaling on Amazon EC2

![image](https://user-images.githubusercontent.com/114364831/212412886-fed2a618-bd1d-49d6-85d5-ac1554f87500.png)

* Vertical scaling -- e.g. t3-medium - server not responding or dropping connection for users, replace with m4.xlarge - but have to shut down server down, add additional resources by changing instance type and spin it back up.This is not the best way... Prefer:
* Horizontal scaling -- leverage elastic load balancing by adding additional instances to handle the demand of the app. E.g. have a t3-medium server, add two more t3-medium servers and rely on horizontal scaling with elastic load balancer to handle process of routing users to correct server. Can leverage auto scaling groups alongside elastic load balancing to make this work.

### Amazon CloudFront

* Leverages AWS edge locations (most prevelant form of AWS global infrastructure)
* **Content delivery network (CDN)** -- servers around the world that you can send your content to
* Enables users to get content from server closest to them
* Supports static and dynamic content
* Includes advanced security features:
  * AWS Shield for DDoS
  * AWS WAF

### Amazon API Gateway

* Fully managed API management service
* Directly integrates with multiple AWS services
* Provides monitoring and metrics on API calls
* Supports VPC and on-premise private applications

### AWS Global Accelerator

* AWS Global Accelerator is a networking service that sends your user's traffic through Amazon Web Service's global network infrastructure, improving your internet user performance by up to 60%.

* Utilizes IP addresses that route to edge locations
* Once request reaches edge locations, traffic is routed through AWS network
* Can route requests to many AWS resources
  * Network Load Balancer (NLB)
  * Application Load Balancer (ALB)
  * EC2 Instances
  * Elastic IP Address
 
### Performance Improvements 
 
* Distance between user and initial endpoint is minimized by using edge locations (same with CloudFront)
* Traffic is optimized by using AWS network instead of public Internet (with IP-based resolution)
* Results in improvement of first byte latency, jitter and throughput (overall more efficient request)
* Provides superior fault tolerance by not relying on DNS solution
  * Most solutions use a host name; IP address of host name might get cached; if using Route 53 for failover, if client needs to failover to a new region, in some cases the switchover may not be seamless (but because of AWS Global Accelerator, it is able to make the transition seamlessly due to IP-based resolution)

### AWS Global Accelerator Use Cases

![image](https://user-images.githubusercontent.com/114364831/212754983-a82a0aea-5fb6-4ace-b27d-648a73e078a6.png)

### Scenario-Based Review

### Scenario 1

Jane's comapny maintains two corporate data centers. They want their data centers to work alongside AWS for specific workloads. She is wondering if there is a way to  have a persistent connection to AWS. What service from AWS would you recommend her company implement?

* AWS Direct Connect (can build direct connections between data centers and AWS; traffic does not need to go over the public internet - communication can happen behind the firewall)

### Scenario 2

Tim's company serves content through their site to users around the globe. They are looking to optimize performance to users around the world. They want to leverage a Content Delivery Network (CDN). Which service would enable optimzed performance globally for their content?

* Amazon CloudFront (CDN present on AWS)

### Scenario 3

Ellen's company has an internal application that runs on an EC2 server. Currently, there is downtime as demand is greater than capacity for the server. Which scaling approach would you recommend and what services should they use?

* Horizontal Scaling ("scaling out") using Elastic Load Balancer
  * Preferable over bigger servers because it can handle future loads; bigger servers may have to be taken down again resulting in downtime to get even bigger servers
  * Elastic Load Balancing routes users to the best server for them to use
