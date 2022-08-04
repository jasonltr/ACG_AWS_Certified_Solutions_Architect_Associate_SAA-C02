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
- Login to aws sandbox account 
- using terminal, enter `aws configure` and enter credentials for the aws sandbox account
- run the eksctl command below (install eksctl [here](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html))
```
jason@DEV-52WP6M3:~/Documents/eks-blue-green$ eksctl create cluster --name fargate-cluster3 --region us-east-1 --zones=us-east-1a,us-east-1b,us-east-1d --fargate
2022-08-04 14:06:07 [ℹ]  eksctl version 0.107.0
2022-08-04 14:06:07 [ℹ]  using region us-east-1
2022-08-04 14:06:07 [ℹ]  subnets for us-east-1a - public:192.168.0.0/19 private:192.168.96.0/19
2022-08-04 14:06:07 [ℹ]  subnets for us-east-1b - public:192.168.32.0/19 private:192.168.128.0/19
2022-08-04 14:06:07 [ℹ]  subnets for us-east-1d - public:192.168.64.0/19 private:192.168.160.0/19
2022-08-04 14:06:07 [ℹ]  using Kubernetes version 1.22
2022-08-04 14:06:07 [ℹ]  creating EKS cluster "fargate-cluster3" in "us-east-1" region with Fargate profile
2022-08-04 14:06:07 [ℹ]  if you encounter any issues, check CloudFormation console or try 'eksctl utils describe-stacks --region=us-east-1 --cluster=fargate-cluster3'
2022-08-04 14:06:07 [ℹ]  Kubernetes API endpoint access will use default of {publicAccess=true, privateAccess=false} for cluster "fargate-cluster3" in "us-east-1"
2022-08-04 14:06:07 [ℹ]  CloudWatch logging will not be enabled for cluster "fargate-cluster3" in "us-east-1"
2022-08-04 14:06:07 [ℹ]  you can enable it with 'eksctl utils update-cluster-logging --enable-types={SPECIFY-YOUR-LOG-TYPES-HERE (e.g. all)} --region=us-east-1 --cluster=fargate-cluster3'
2022-08-04 14:06:07 [ℹ]  
2 sequential tasks: { create cluster control plane "fargate-cluster3", 
    2 sequential sub-tasks: { 
        wait for control plane to become ready,
        create fargate profiles,
    } 
}
2022-08-04 14:06:07 [ℹ]  building cluster stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:06:09 [ℹ]  deploying stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:06:39 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:07:10 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
```