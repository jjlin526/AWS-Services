### Amazon Route 53

A reliable and cost-effective way to **route end users to Internet applications**.

* Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service. Route 53 connects user requests to internet applications running on AWS or on-premises (maps domain names to internal AWS services)
* Route end users to a site reliably with globally-dispersed Domain Name System (DNS) servers and automatic scaling
* Set up your DNS routing in minutes with domain name registration and straightforward visual traffic flow tools
* Customize DNS routing policies to reduce latency, improve application availability, and maintain compliance

### Domain Name System

* System that translates human-readable URLs to IP addresses so that two computers can connect
* EC2 instances can be configured with public IP addresses
* S3 buckets and load balancers are more complicated because they do not have static visible IP addresses

Route 53 allows a client to set up URL resolution to AWS resources directly, bypassing the need to see an IP
* IP resolution happens behind the scenes, but Route 53 abstracts this away
* Route 53 is core to letting users interact with services in AWS 
* Route 53 lets URLs resolve to AWS services

![Route-53](https://user-images.githubusercontent.com/114364831/211432301-cecba3c0-71ff-4398-ab5a-5a3ad522f6e4.png)
