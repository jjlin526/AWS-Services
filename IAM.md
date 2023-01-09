### AWS Identity and Access Management (IAM)
* Deals with identity and authorization
* Whenever you try to achieve any action on AWS, you have to go through IAM which will identify you and then allow or deny the action depending on the rights that have been granted to you by your account administrator
* For example, when you connect to the AWS web console, it is IAM that checks your login and password and allow you to access your account
* When you try to create a new EC2 instance, it is IAM that checks that the rights needed to carry this action have been granted to you by your account administrator
* When anpplication tries to access a resource hosted on AWS: IAM will identity the application using the access key provided and will check that the action is indeed authorized
