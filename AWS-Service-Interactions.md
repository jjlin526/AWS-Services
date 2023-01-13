### AWS Service Interactions

![image](https://user-images.githubusercontent.com/114364831/212338172-1a962620-b69b-4821-b9b5-36ba00983114.png)

### AWS Management Console

* A web and app based interface for interacting with all of the 150+ AWS services. All major browsers and mobile operating systems are supported.

### AWS Command Line Interface (CLI)

* Tool to manage your use of AWS services from the command line on Windows, Mac, and Linux. Almost every task that can be done in the console can be done in the CLI.

### Using the AWS CLI

``` aws iam list-users ```

![image](https://user-images.githubusercontent.com/114364831/212338951-b81a376b-cdc6-44b8-bed9-9039152a613b.png)

* Does not include the root user; limited to the iam users

### AWS Software Developer Kit (SDK)

* Programming language-specific resources that allow you to interact with AWS services via code. This approach enables you to **automate** many aspects of how you interact with the platform.

### AWS SDK Languages

![image](https://user-images.githubusercontent.com/114364831/212339894-4cb60d9a-028b-4fc3-83c8-510bb496df70.png)

### Interacting with AWS

* Console is a great method for testing out AWS services
* Repeated tasks can be automated using the CLI or SDK
* SDK enables automation of AWS tasks within custom applications (custom application running on AWS and want to automate interaction with some AWS service)
* Most services and actions can be performed in any of the three

### Using the AWS CLI

1. Create access keys (access key, secret access key) for IAM user
2. Install AWS CLI or use AWS CloudShell
3. Configure AWS CLI to use credentials created
4. Access some AWS resources like S3 buckets created within the account: i.e. `aws s3 ls --profile pstest`
