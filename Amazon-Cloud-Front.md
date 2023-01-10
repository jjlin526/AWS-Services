### Amazon CloudFront

* Content Delivery Network (CDN) that allows serving of files globally with fast connections and limited latency
* Works seamlessly with S3, EC2, AWS Load Balancers and Route53 to serve content from a location closest to incoming requests

### CloudFront Structure

* Start by creating a distribution (a set up of content to be served from CloudFront)
* Need to specify an original location for the content (i.e. an S3 bucket)
* Once a distribution has been created, a unique CloudFront URL will be assigned to the distribution (used to access the content)

### CloudFront Configuration Options

* SSL certificates
* Allowed HTTP methods
* Edge locations
* 
