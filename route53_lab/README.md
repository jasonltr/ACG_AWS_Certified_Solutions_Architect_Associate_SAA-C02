## ACG_AWS_Certified_Solutions_Architect_Associate_SAA-C02

I will be documenting my process of the AWS Solutions Architect course from [Acloudguru](https://learn.acloud.guru/course/aws-certified-solutions-architect-associate/overview) here

All content is from acloudguru

Main topics to focus on are
- S3
- Route 53
- VPC

Try to document lab exercises to show proof of concepts

## Route 53
- Starts from slide 567 [.pdf](/1621966269571-AWS%20Certified%20Solutions%20Architect%20Associate%20SAA-C02%20NEW%20PDF_compressed.pdf)

### DNS 101 Domain Name System
- it is a phonebook
- you enter something easy to remember, refer to DNS, get the actual address of the resource

### Register a Domain Name
- register a domain name
- create 3 EC2 instances in 3 different locations
- need to create Security group for each of the instances
- using bootstrap script that launches a simple website with a text msg
![](/route53_lab/images/53_1.png)
![](/route53_lab/images/53_2.png)

### Simple routing
- get the public IP of your instances
- route53 > create record set > enter type A record and the 3 ip addresses
![](/route53_lab/images/53_3.png)
- test the domain name that was bought
![](/route53_lab/images/53_4.png)
- varying the TTL will show a different instance after that time set
- simple routing policy only allows one record with multiple IP addresses
- if multiple IP addresses are in a record, route53 returns all values in a random order

### weighted routing policy
- weigh a certain % of traffic to a specific instance
- delete the previous A record
- create record set > paste IP addresses > select weighted for routing policy > essentially multiple records for the domain name with the desired weights
![](/route53_lab/images/53_5.png)
