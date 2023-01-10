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

### How to Set Up Route 53

* Set up a Hosted Zone (route domain name like example.com or google.com)
* Use Hosted Zone to set up subdomains like www.example.com or mail.example.com and configure them to route to AWS resources
* Can create records sets like A records, CNAME Records and MX Records for subdomains
  * A records map a domain name to an IP address. When someone types a domain name into their web browser, the A record is used to find the website's IP address so that the browser can connect to it
  * CNAME records are used to create an alias for a domain name. This allows you to use a different name, such as a subdomain, to access the same website
  * MX records are used to configure email delivery for a domain. They specify the mail servers that are responsible for accepting email messages sent to that domain

### Route 53 Health Checks
* Set up regular checks for a given URL path
* Health Checks sends alerts based on different rules (i.e. URL request gets a response of 404 or 503) -- essential tool for customer-facing web application

![Route-53](https://user-images.githubusercontent.com/114364831/211432301-cecba3c0-71ff-4398-ab5a-5a3ad522f6e4.png)
