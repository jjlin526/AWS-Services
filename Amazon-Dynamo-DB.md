### Amazon DynamoDB

* Managed **NoSQL database service** from AWS 
* Supports document and key-value store models
* Has good scalability and flexibility 

### DynamoDB Features

* Unlimited, elastic storage (EBS size not considered)
* No hardware choices (EC2 instance choice required for RDS)
* Pay only for what you use (what you store and how often it is queried)
* Guaranteed high performance with queries regardless of read/write units that have been provisioned

### DynamoDB Base Structure

* Table is root point for data storage
* Each table needs a primary key for indexing and retrieval
* Optionally secondary indexes

### Provisioned Throughput Capacity

* **Provisioned Throughput Capacity** = Number of Read/Write Units per second
* Each read unit is limited to 4kb/unit
* Each write unit is limited to 1kb/unit
* Any requests over the above limits consumes additional units

### More on Provisioned Throughput Capacity

* In AWS Lambda, provisioned throughput capacity is a feature that allows a client to provision a specific number of requests per second (RPS) for a given function
* This feature is useful when a function is expected to receive a large number of requests and a client wants to ensure that it can handle the load
* When a client enables provisioned throughput capacity for a function, the number of requests per second (RPS) is specified to provision for the function. Once a certain number of RPS has been provisioned, the function will be able to handle that number of requests per second, regardless of any burst traffic that might occur.
* Provisioned throughput capacity is not the same as concurrency. Concurrency, refers to the number of requests being served at any given point in time, while RPS (Requests per second) is a metric that measures the number of requests that are handled by your function over a period of time
* Provisioned throughput capacity is mainly useful in the case of high-traffic and/or real-time functions, like gaming, financial services or online marketplaces, that need to handle a large number of requests in a short period of time

### DynamoDB Pricing

* Depends on Provisioned Throughput Capacity, amount of data stored and region
