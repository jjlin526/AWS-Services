### AWS

* Collection of cloud computing services
* Can work together or independently
* Runs or supports a computer program
* Provides computing, routing, storage, networking, etc.
* AWS is a provider of Cloud Services

### Why depend on AWS?

* **Cost**: Without AWS, a user needs to buy a server to serve web application, a server for the database, cables to hook it up to a broadband connection and a dedicated room to house the hardware. On AWS, there are no upfront costs for most services.
* **Scalability**: Without AWS, a user must scale up by ordering another server. By deploying to AWS, scalability is resolved. Adding a server takes a few clicks - no upfront costs to spin up new instance of web application.

### Why deploy globally?

* Reduce **latency**: latency (time to get bits from server to a user's browser and vice versa; biggest contributor is physical distance from server to user) affects the user experience. Self-hosting provides no control over distance from server to user. AWS has the most data servers out of all cloud service providers, and thus solves the latency problem best.
* Increased **redundancy**: AWS has many **Regions** (physical locations where certain services are hosted) which are composed of **Availability Zones** (collection of data centers with completely separate power, networking and connectivity connected using hyper-fast fibre optics). Availability Zones are very fault tolerant - if someone forgets to pay the electricity bill at one data center, the others provide a redundant failover. Scaling across Regions and AZ's increases redundancy.

### How does AWS work?

* Services interact with each each other using TCP. Port depends on service used
* A client initiates connection to services by making requests to AWS services
* If all service instances are made in the same VPC, then they will have local IP addresses which enable fast connections
* Security Groups act as firewalls between instances

### AWS vs. the Rest

* **Microsoft Azure**: both AWS and Azure have robust service offerings and strong global reach. Best place to run Microsoft products. AWS has a better web console (Azure interface is more cluttered)
* **Google Cloud Platform**: specializations in Big Data, Kubernetes and AI. Both AWS and GCP have strong global reach. AWS has 12x more market share and better web console
* **Heroku**: Heroku app deployment is very simple but it lacks the breadth and reach (only 8 regions) of AWS
