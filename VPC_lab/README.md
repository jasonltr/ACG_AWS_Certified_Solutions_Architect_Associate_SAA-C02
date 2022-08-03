## ACG_AWS_Certified_Solutions_Architect_Associate_SAA-C02

I will be documenting my process of the AWS Solutions Architect course from [Acloudguru](https://learn.acloud.guru/course/aws-certified-solutions-architect-associate/overview) here

All content is from acloudguru

Main topics to focus on are
- S3
- Route 53
- VPC

Try to document lab exercises to show proof of concepts

- [ACG_AWS_Certified_Solutions_Architect_Associate_SAA-C02](#acg_aws_certified_solutions_architect_associate_saa-c02)
- [VPC](#vpc)
- [create a vpc and subnet](#create-a-vpc-and-subnet)
- [creating instances in each subnet](#creating-instances-in-each-subnet)
- [testing connectivity between instances across subnets](#testing-connectivity-between-instances-across-subnets)
- [NAT Gateway](#nat-gateway)

## VPC
- Starts from slide 626 [.pdf](/1621966269571-AWS%20Certified%20Solutions%20Architect%20Associate%20SAA-C02%20NEW%20PDF_compressed.pdf)

![](/VPC_lab/images/vpc_1.png)

## create a vpc and subnet
- using aws console create a vpc
![](/VPC_lab/images/vpc_3.png)
- this is what we have created so far, SG, NACL and RT are created automatically with default settings
![](/VPC_lab/images/vpc_2.png)
- create two subnets
![](/VPC_lab/images/vpc_4.png)
![](/VPC_lab/images/vpc_5.png)
- create internet gateway and attach to your vpc
- you can only have one internet gateway attached to one vpc
- go to route table to create a new route table for public subnets only
- configure that route table, edit route and add 0.0.0.0/0 as destination, target is internet gateway
![](/VPC_lab/images/vpc_6.png)
- go to subnet association, select 10.0.1.0/24, this instance will now be exposed to public via internet
- the original route table will have 10.0.2.0/24 but no longer have 10.0.1.0/24

## creating instances in each subnet 
- we now have a public subnet, and a private subnet
- next will be creating instances in each of these subnets
- one instance for public subnet, one instance for private subnet
- new SG for the instance in public subnet
![](/VPC_lab/images/vpc_9.png)
- this is what we have created so far
![](/VPC_lab/images/vpc_8.png)


## testing connectivity between instances across subnets
- create new SG to allow communication between instance1 in public subnet with instance2 in private subnet via private IP
![](/VPC_lab/images/vpc_10.png)
- go to instances and change instance2 sg to the sg that was just created
![](/VPC_lab/images/vpc_11.png)
- connect to instance1 via ec2 instance connect
- ping private IP of instance 2 
![](/VPC_lab/images/vpc_12.png)

## NAT Gateway
- allow instances in the private subnet to access internet 
![](/VPC_lab/images/vpc_13.png)
- create NAT gateway in the public subnet
- go to main route table (private subnet) and edit route
- add 0.0.0.0/0 target the NAT gateway that was just created
![](/VPC_lab/images/vpc_14.png)
- ssh into instance1, then from instance 1 ssh into instance2
![](/VPC_lab/images/vpc_15.png)
- try to install packages (to test the NAT gateway is working)
![](/VPC_lab/images/vpc_16.png)
- Success!

