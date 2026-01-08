# VPC Endpoints
# -y Samhitha Bhoopesh
**Author:** samhithabbb@gmail.com  
**Email:** samhithabbb@gmail.com

---

## VPC Endpoints

![VPC Endpoint Overview](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today’s Project!

### What is Amazon VPC?

In this project, I demonstrated how to build a secure AWS network by creating a VPC, launching an EC2 instance, creating an S3 bucket, and configuring a VPC endpoint. This project focuses on private networking and secure access to AWS services without using the public internet, which is a critical skill for cloud and DevOps roles.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create an isolated network environment where my EC2 instance could securely communicate with Amazon S3. I controlled routing, connectivity, and access using subnets, route tables, and VPC endpoints.

### One thing I didn’t expect in this project was…

One thing I didn’t expect in this project was how access to S3 could be completely blocked or allowed simply by modifying bucket policies and route tables. This showed how closely networking and security work together in AWS.

### This project took me…

This project took me approximately 1–1.5 hours to complete, including testing connectivity and validating endpoint configurations.

---

## In the first part of my project…

### Step 1 – Architecture set up

In this step, I created a Virtual Private Cloud (VPC) because a VPC provides an isolated and secure network environment where AWS resources can communicate privately.

### Step 2 – Connect to EC2 instance

In this step, I launched an EC2 instance inside my VPC because EC2 provides compute resources that allow me to run AWS CLI commands and test network connectivity.

### Step 3 – Set up access keys

In this step, I configured AWS access keys on my EC2 instance because access keys allow the instance to authenticate and interact with AWS services like Amazon S3.

### Step 4 – Interact with S3 bucket

In this step, I created an S3 bucket because Amazon S3 allows me to store objects and test how my EC2 instance interacts with AWS services.

---

## Architecture set up

I started my project by launching a VPC with a public subnet and an EC2 instance inside that subnet.

I also created an S3 bucket that I would later access from my EC2 instance to test permissions and networking behavior.

![Architecture Setup](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To allow my EC2 instance to interact with AWS services, I configured AWS access keys using the AWS CLI.

Access keys are credentials that allow programmatic access to AWS services.

Secret access keys act like passwords and must be kept secure because they grant access based on assigned permissions.

### Best practice

Although I used access keys in this project, a best practice alternative is to use IAM roles attached directly to EC2 instances, which removes the need for long-term credentials.

---

## Connecting to my S3 bucket

The command I ran was:

aws s3 ls

This command lists all S3 buckets available to the authenticated user.

The terminal returned a list of buckets, indicating that the access keys were configured correctly.

![S3 Bucket Access](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket (continued)

I also tested the command:

aws s3 ls s3://<bucket-name>

This returned the contents of my bucket, confirming that my EC2 instance could successfully access the S3 bucket.

![S3 Bucket Listing](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first created a file on my EC2 instance.

I then ran the command:

aws s3 cp <file-name> s3://<bucket-name>

Finally, I validated the upload by running:

aws s3 ls s3://<bucket-name>

![Uploading Objects](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project…

### Step 5 – Set up a Gateway

In this step, I created an S3 Gateway VPC Endpoint because it allows private communication between my VPC and Amazon S3 without using the public internet.

### Step 6 – Bucket policies

In this step, I updated my S3 bucket policy to restrict access and enforce that all requests must go through the VPC endpoint.

### Step 7 – Update route tables

In this step, I updated my route tables to ensure traffic destined for S3 was routed through the VPC endpoint.

### Step 8 – Validate endpoint connection

In this step, I validated that my EC2 instance could access S3 only through the VPC endpoint, confirming secure and private connectivity.

---

## Setting up a Gateway

I set up an S3 Gateway endpoint, which allows resources in a VPC to access Amazon S3 privately without requiring an internet gateway or NAT device.

### What are endpoints?

An endpoint is a private connection between a VPC and an AWS service that keeps traffic within the AWS network.

![Gateway Endpoint](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a resource-based policy that controls who can access an S3 bucket and under what conditions.

My bucket policy restricted access so that only traffic originating from the VPC endpoint could access the bucket.

![Bucket Policy](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies (continued)

After saving my bucket policy, the S3 console showed “denied access” warnings because public and non-endpoint access was intentionally blocked.

I also updated my route table to ensure traffic from my subnet could reach S3 through the VPC endpoint.

![Policy Warning](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my route table, I associated it with the VPC endpoint so traffic destined for Amazon S3 would use the private route.

After updating the route table, my EC2 instance could successfully access the S3 bucket again.

![Route Table Update](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy controls what actions are allowed through a VPC endpoint.

I updated my endpoint policy to restrict specific S3 actions, and I could immediately see the effect when some operations were allowed while others were denied.

![Endpoint Policy](http://learn.nextwork.org/motivated_cyan_peaceful_tiger/uploads/aws-networks-endpoints_3e1e79a3)
