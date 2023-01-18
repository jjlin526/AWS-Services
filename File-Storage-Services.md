### File Storage Services

### AWS File Storage and Data Transfer Services

![image](https://user-images.githubusercontent.com/114364831/212757260-e1e99132-fb67-4d56-a814-37768664955b.png)

### Overview

### Amazon Simple Storage Service (S3)

* Stores files as objects in buckets
    * Buckets are the unit of organization within S3. You will create a bucket with a set of settings; any file that you drop in has those settings applied to it.
* Provide different storage classes for different use cases
* Stores data across multiple availability zones (durability and resiliency for data)
* Enables URL access for files
* Offers configurable rules for data lifecycle
    * If you want something to expire after a given time or go to a different storage class
* Can serve as a static website host

### Amazon S3 Non-archival Storage Classes

![image](https://user-images.githubusercontent.com/114364831/212760937-bd28347d-23ac-4aa4-9c3e-9d77116931c4.png)

### S3 Intelligent Tiering Storage Class

* Automatically move files based on access
* Moves between frequent and infrequent access
* Same performance as S3-Stanard (can provide cost savings if you have some data that needs to be moved between storage classes)

### S3 Lifecycle Policies

* Objects in a bucket can transition or expire based on your criteria (cannot move an object back on forth based on usage -- only available with **Intelligent Tiering**)
* Transitions can enable objects to move to another storage based on time (i.e. can configure a certain file to last for 30 days based on **Lifecycle Policies**)
* Expiration can delete objects based on age 
* Policies can also factor in versions of a specific object in the bucket (i.e. can delete a version of the file that is not the current version after 7 days)

### S3 Transfer Acceleration

* Feature that can be enabled per bucket that allows for optimized uploading of data using the AWS Edge Locations are part of Amazon CloudFront -- (upload data in a fast and efficient way into S3 buckets)
