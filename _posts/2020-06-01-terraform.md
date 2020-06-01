---
layout: post
title: Postman walkthrough HTB 
---

![](/images/2020-06-01-terraform/0.png)

Hey guys, In this tutorial I wanted to share how we can spin up an ec2 instance in amazon using terraform. 

Terraform by HashiCorp provides a lot of example templetes for provising cloud platform such as AWS and Azure. However, we I tried to use the templete I encountred number of errors and was confused about where to find some of the things mentioned in the templete.

Here is the basic templete by HashiCorp: https://www.terraform.io/docs/providers/aws/r/instance.html

For this tutorial I will be using a MacOS, So first we need to install terraform:
 
```
$ brew install terraform

```
For any other OS, refer : https://learn.hashicorp.com/terraform/getting-started/install.html


This is how I spun up an ec2 instance in less than a minute: 

Step 1: Create a file with .tf extension with the content below 

```
provider "aws" {
	region = "us-east-1"
	access_key= "AK*******"
	secret_key= "W*******"
}

resource "aws_instance" "web" {
	ami = "ami-085925f297f89fce1"
	instance_type = "t2.micro"
	key_name = "cons****"
	associate_public_ip_address = true

tags = {
	Name = "test1"
	Owner = "san3ncrypt3d"
}
}

```

Step 2: 

```
terraform plan 
```

At this point you will see all the specifications of the instance you are going to create. It is imperative that you review and understand that the specifications displayed are what you desire to create.


![](/images/2020-06-01-terraform/1.png)

The next step is to apply these:

Step 3: 

```
terraform apply 
```
![](/images/2020-06-01-terraform/2.png)

Now the instance is going to be created.

Before procceding, terraform is going to ask you to confirm this by tying "yes"

![](/images/2020-06-01-terraform/3.png)


Now you'll have the ec2-instance created 

![](/images/2020-06-01-terraform/4.png)


Appendix:

1) Where can you find the access key and secret key ?

Step 1: Go to your AWS console
Step 2: Search for "IAM"
![](/images/2020-06-01-terraform/4.png)

Step 3: click on "users"
Step 4: At this point you can create a new user to get access key and secret key or click on the existing user to get the creds.

![](/images/2020-06-01-terraform/6.png)


2) Where can you find the ami-id ?

You can find any ami-id of images on AWS by "Amazon EC2 AMI Locator" - https://cloud-images.ubuntu.com/locator/ec2/

![](/images/2020-06-01-terraform/7.png)

3) what is key_name ?

key_name is the essentially same as what is known to be "key pair" in AWS. So you will be using the mentioned key_name to ssh into your newly created instance.

4) Where can you find the key pair in AWS?

Step 1: Go to your aws console.Under "NETWORK & SECURITY", click on "key pair" and choose a key pair you have access to.

![](/images/2020-06-01-terraform/8.png)
![](/images/2020-06-01-terraform/9.png)


If you encounter any issue or need any assistance, ping me :)



