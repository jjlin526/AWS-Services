### AWS Identity and Access Management (IAM)
* Deals with **identity and authorization**
* Whenever you try to achieve any action on AWS, you have to go through IAM which will identify you and then allow or deny the action depending on the rights that have been granted to you by your account administrator
* For example, when you connect to the AWS web console, it is IAM that checks your login and password and allow you to access your account
* When you try to create a new EC2 instance, it is IAM that checks that the rights needed to carry this action have been granted to you by your account administrator
* When anpplication tries to access a resource hosted on AWS: IAM will identity the application using the access key provided and will check that the action is indeed authorized

### Accounts
* It is common for an organization to possess a number of AWS accounts, in order to separate each different environment. One account could host the development environment, another could host the staging environment and the last one could host the production environment

### Users
* A user is an AWS entity associated with an individual or with an application. A user has identification information in the form of a username and password pair or an access key.

### Requests
* Each AWS action , whether it originates from the web console, the CLI AWS tool or from some piece of software creates a request sent to AWS 
* The IAM service will compare that request with the list of permissions - the policies – defined by the account administrator to determine whether or not the action is allowed

The three main fields specified in a request are the principal, the action and the resource
* Principal: User or role who requested permission
* Action: Operation that the principal requests to make on the resource. The name of these actions is composed of the three letters’ name of a service and the name of the action beginning by a verb.

```
"Action" : "ec2:StartInstances"
"Action" : "iam:ChangePassword"
```

* Resource: Target of the action.

Almost anything that exists on AWS is a resource. E.g. an EC2 instance, a role, or the RDS service

```
"Resource" : "arn:aws:iam::012345678912:user/Alice"
```

The user Alice of the account 012345678912

```
"Resource" : "arn:aws:sqs:eu-west-1:012345678912:queue1"
```

The queue queue1 of the account 012345678912 in the region eu-west-1

The formats of those identifiers are not exactly the same:
* The region is specified for the SQS resource but not for the IAM resource. This is because the IAM service is trans-region and the SQS service is not.
* The resource type is specified for the IAM resource but not for the SQS resource. There are a few types of resources in the IAM service (users, groups, roles, policies...) whereas there are only queues in SQS

ARNs (Amazon Resource Names) are created to identify a resource in a unique way.

### Policies

A policy is a rule controlling a user, a group or a role access to a resource.

The policy defines the Action and Resource fields and adds an Effect field that indicates whether the action should be allowed or denied.

Policy in JSON format:

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Action": "ec2:*",
    "Effect": "Allow",
    "Resource": "*"
  }
}
```

This policy allows any EC2 action. 

It is also possible to encounter policies specifying a Principal field instead of a Resource field when talking about a trusted relationship:

```

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": { "Service": "ds.amazonaws.com" },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

This example allows Amazon Directory Service to assign this role to its users. It would also be possible to allow users from another AWS account to use this role with a similar trust relationship.

* A policy is in effect only when it is attached to an IAM entity (user, group or role)
* When a policy specifying a Resource is attached to a user, this user is the Principal of the action
* On the contrary, if the policy specifies a Principal, it should be understood that the entity it is attached to is the Resource

Diagram illustrating the use of strategies:  

![image](https://user-images.githubusercontent.com/114364831/211383877-d0171df2-1e2c-40b1-827a-6d019da4af12.png)

For the diagram above:
* Bob can make any RDS action on any resource
* Alice can make the rds:DescribeDBInstances on any resource. However, she tries to make another action (rds:StartDBInstance). Therefore her request is rejected.
* Anne can make any RDS action on the resource identified by its ARN.
* Mehdi can make any RDS action on any resource but one specific resource identified by its ARN. He still tries to act on this resource. His request is rejected.

**When both a policy allowing access and another denying it can be applied to the same resource, the access is denied.**

### Roles

* A role is an AWS entity that can be compared to a user. However, a role is usually not associated with an individual or a precise application. 
* Many users are usually given the right to assume a role (i.e. use temporarily the rights associated with a role)
* A role, contrarily to a user does not have a password and uses temporary identification information.
* Generic roles are already created on IAM and are directly available but it is possible to create new ones to deal with a precise need. Those generic roles are already associated with generic policies.

A role could be used to allow users from a different account to act on resources on the role’s account.

Diagram showing direct access to a resource from another account:  

![image](https://user-images.githubusercontent.com/114364831/211385712-d0d22b74-90bd-43e4-9885-b6a835a90702.png)

* Bob and Alice try to act directly on a resource hosted on an account different from theirs; their requests are rejected.
* Anne can make any RDS action on any resource and is in the same account as the resource she tries to act upon.

**It is necessary to assume a role to act on a resource on a different account.**

Diagram showing access to a resource from another account through a role  

![image](https://user-images.githubusercontent.com/114364831/211388796-ce18c1f4-b313-4b36-ac40-faf2c2647094.png)

* Bob and Anne do not have a policy that allows them to male the action sts:AssumeRole. Their requests are rejected.
* Alice can make the sts:AssumeRole on a specific role identified by its ARN. Her request is allowed and she can then use the role to make the action rds:StartDBInstance.
