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

### Scenario-based Review

1. Roger's comapny runs several production workloads in AWS. They have a new web application that manages digital assets for marketing. They need to automatically create a user account in Amazon Cognito (user directory for custom application) on sign-up. They want this to seamlessly integrate into the application (React-based web application with microservices in back-end written in Node.js). Which interaction method would Roger's company use for this?

* Software Development Kit (SDK) -- bake into custom application (can leverage SDK to enable Node.js to interact with Amazon Cognito within his web app)

2. Eliza's company is considered transitioning to AWS. They want to leverage Amazon Relational Database Service. Eliza wants to test out a single database on the service. What interaction method would Eliza use for this use case?

* AWS Console (no automation, not for production - just get in and use the service)

3. Jennier's company is a startup. They created a social network for entrepreneurs with a web and mobile app. Jennifer has a set of tasks she needs to run on AWS each day to generate reports. What interaction method would Jennifer use for this use case?

* Command Line Interface (CLI -- i.e. custom script) - or SDK for automation (back it into a custom application using one of the support programming languages)
