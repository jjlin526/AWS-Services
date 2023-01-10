### Amazon S3

Amazon Simple Storage Service (Amazon S3) is an **object storage service** offering industry-leading scalability, data availability, security, and performance.
* Customers of all sizes and industries can store and protect any amount of data for virtually any use case, such as data lakes, cloud-native applications, and mobile apps
* Maximum file in 5 terabytes; maximum file size that can be uploaded in a single PUT operation is 5 gigabytes

### Object Storage

* Data is stored redundantly across multiple storage servers
* Object Storage actively monitors data integrity using checksums and automatically detects and repairs corrupt data

The diagram shows how to move data to Amazon S3, manage stored data in Amazon S3, and analyze data with other services. Three sections display from left to right.  

![image](https://user-images.githubusercontent.com/114364831/211413856-4cca1270-2c5f-441f-8989-c233918dd239.png)

### Buckets

* **Buckets** are the foundational structure in S3
* Root resource that can be used to add, delete and modify objects
* Can set permissions, hosting options and logging

### S3 Buckets Can

* Trigger events when objects are added/modified/deleted
* Preserve older versions of objects
* Replicate objects across regions

S3 buckets are accessed via URL
* S3 Bucket Region - Bucket Name - Object Path

When the permissions of objects are modified to allow anonymous access, S3 can be used to host static files for websites  

* Within the bucket configuration options, there is the ability to enable static website hosting for the given bucket (an S3 Hosted Website URL)
* Still have object level permissions to give access to anonymous and authenticated users
* Bucket itself will respond to requests and be enabled to interact with Route 53 URLs
* Fast way to get a static website up with minimal costs

### How to Solve Latency in S3

* S3 can automatically replicate files to other regions

Step 1: Use CloudFront (can cache content -- edging content in locations around the world)

### S3 Pricing Structure

* Pricing based on 
  * Amount of data stored
  * Number of requests
  * Amount of data transferred
  * Region
