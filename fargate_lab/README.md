## ACG_AWS_Certified_Solutions_Architect_Associate_SAA-C02

I will be documenting my process of the AWS Solutions Architect course from [Acloudguru](https://learn.acloud.guru/course/aws-certified-solutions-architect-associate/overview) here

All content is from acloudguru

Try to document lab exercises to show proof of concepts

### what is fargate
![](/fargate_lab/images/fargate_1.png)
![](/fargate_lab/images/fargate_2.png)
![](/fargate_lab/images/fargate_3.png)
- AWS owns and manages infrastructure
- still need ECS,EKS
- need to compare with EC2
![](/fargate_lab/images/fargate_4.png)

### create ECR push simple image in
- follow steps from [blue green deployment POC](https://github.com/jasonltr/eks-blue-green) to get parrot images into ECR
![](/fargate_lab/images/fargate_5.png)

### use ECS + Fargate to launch the parrot image/website
- on AWS console > ECS > Task Definitions > Create New Task Definition > Fargate
![](/fargate_lab/images/fargate_6.png)
- set cpu limits
![](/fargate_lab/images/fargate_8.png)
- enter the uri of the image pushed earlier
![](/fargate_lab/images/fargate_7.png)
- clusters > create clusters > networking only (no instances)
- view cluster > Tasks tab > run new task
- launch type fargate, task definition is the task created previously
![](/fargate_lab/images/fargate_9.png)
- default for everything under VPC
![](/fargate_lab/images/fargate_10.png)
- launch the task, wait awhile for it to be running, check the details of the task, get the public IP, check the logs, it says listening on port 3000
![](/fargate_lab/images/fargate_11.png)
![](/fargate_lab/images/fargate_12.png)
- go to the publicurl:port and check
![](/fargate_lab/images/fargate_13.png)
- success! website/image is launched without creation of any instance
- note that ECS cluster was still created

### use EKS + fargate to launch the parrot image/website
- use terraform script from previous POC to create EKS cluster and its dependencies. (VPC,subnets,route tables etc)

```
Apply complete! Resources: 52 added, 0 changed, 1 destroyed.

Outputs:

cluster_endpoint = "https://5BC90AFAF203F02570B3DEBC11AAC51A.gr7.us-east-1.eks.amazonaws.com"
cluster_id = "eks-blue-green"
cluster_name = "eks-blue-green"
cluster_security_group_id = "sg-038311c99395cbef4"
config_map_aws_auth = [
```