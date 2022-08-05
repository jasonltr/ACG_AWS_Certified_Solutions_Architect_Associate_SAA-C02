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

### use EKS + fargate to launch the parrot image/website [tutorial](https://www.youtube.com/watch?v=DLmKMBZ_m3w)
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
2022-08-04 14:08:11 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:09:13 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:10:14 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:11:16 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:12:17 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:13:18 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:14:20 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:15:21 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:16:22 [ℹ]  waiting for CloudFormation stack "eksctl-fargate-cluster3-cluster"
2022-08-04 14:18:32 [ℹ]  creating Fargate profile "fp-default" on EKS cluster "fargate-cluster3"
2022-08-04 14:22:54 [ℹ]  created Fargate profile "fp-default" on EKS cluster "fargate-cluster3"
W0804 14:23:26.723248    2959 warnings.go:70] spec.template.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].key: beta.kubernetes.io/os is deprecated since v1.14; use "kubernetes.io/os" instead
W0804 14:23:26.723303    2959 warnings.go:70] spec.template.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[1].key: beta.kubernetes.io/arch is deprecated since v1.14; use "kubernetes.io/arch" instead
2022-08-04 14:23:26 [ℹ]  "coredns" is now schedulable onto Fargate
2022-08-04 14:24:33 [ℹ]  "coredns" is now scheduled onto Fargate
2022-08-04 14:24:33 [ℹ]  "coredns" pods are now scheduled onto Fargate
2022-08-04 14:24:33 [ℹ]  waiting for the control plane availability...
2022-08-04 14:24:33 [✔]  saved kubeconfig as "/home/jason/.kube/config"
2022-08-04 14:24:33 [ℹ]  no tasks
2022-08-04 14:24:33 [✔]  all EKS cluster resources for "fargate-cluster3" have been created
2022-08-04 14:24:36 [ℹ]  kubectl command should work with "/home/jason/.kube/config", try 'kubectl get nodes'
2022-08-04 14:24:36 [✔]  EKS cluster "fargate-cluster3" in "us-east-1" region is ready
```
```
jason@DEV-52WP6M3:~/Documents/eks-blue-green$ kubectl get nodes
NAME                                      STATUS   ROLES    AGE    VERSION
fargate-ip-192-168-102-219.ec2.internal   Ready    <none>   2m5s   v1.22.6-eks-14c7a48
fargate-ip-192-168-163-147.ec2.internal   Ready    <none>   117s   v1.22.6-eks-14c7a48
jason@DEV-52WP6M3:~/Documents/eks-blue-green$ kubectl get pod --all-namespaces
NAMESPACE     NAME                       READY   STATUS    RESTARTS   AGE
kube-system   coredns-5d5bcc87bc-lpxj6   1/1     Running   0          6m43s
kube-system   coredns-5d5bcc87bc-slbvc   1/1     Running   0          6m42s
```
- note these nodes are not visible in the ec2 page in aws console
![](/fargate_lab/images/fargate_17.png)
- try deploying a nginx image
```
jason@DEV-52WP6M3:~/Documents/eks-blue-green$ kubectl create deployment nginx --image=nginx
deployment.apps/nginx created
```
cheeck progress of node/pod creation
```
jason@DEV-52WP6M3:~/Documents/eks-blue-green$ kubectl get pod --all-namespaces -w
NAMESPACE     NAME                       READY   STATUS    RESTARTS   AGE
default       parrot-7b4bb89695-r46tz    0/1     Pending   0          24s
kube-system   coredns-5d5bcc87bc-lpxj6   1/1     Running   0          15m
kube-system   coredns-5d5bcc87bc-slbvc   1/1     Running   0          15m
default       parrot-7b4bb89695-r46tz    0/1     Pending   0          52s
default       parrot-7b4bb89695-r46tz    0/1     ContainerCreating   0          52s
default       parrot-7b4bb89695-r46tz    1/1     Running             0          61s
default       nginx-6799fc88d8-lsjg5     0/1     Pending             0          0s
default       nginx-6799fc88d8-lsjg5     0/1     Pending             0          1s
default       nginx-6799fc88d8-lsjg5     0/1     Pending             0          54s
default       nginx-6799fc88d8-lsjg5     0/1     ContainerCreating   0          54s
default       nginx-6799fc88d8-lsjg5     1/1     Running             0          61s
```
```
jason@DEV-52WP6M3:~/Documents/eks-blue-green$ kubectl get nodes -w
NAME                                      STATUS   ROLES    AGE     VERSION
fargate-ip-192-168-102-219.ec2.internal   Ready    <none>   57m     v1.22.6-eks-14c7a48
fargate-ip-192-168-128-180.ec2.internal   Ready    <none>   8m28s   v1.22.6-eks-14c7a48
fargate-ip-192-168-134-173.ec2.internal   Ready    <none>   42m     v1.22.6-eks-14c7a48
fargate-ip-192-168-163-147.ec2.internal   Ready    <none>   57m     v1.22.6-eks-14c7a48
```
```
jason@DEV-52WP6M3:~/Documents/eks-blue-green$ kubectl create service nodeport nginx --tcp=80:80
service/nginx created
```
```
jason@DEV-52WP6M3:~/Documents/eks-blue-green$ kubectl exec nginx-6799fc88d8-lsjg5 -- curl -sS localhost:80/
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
- again to reiterate, there is nothing being created on ec2 


### try deploy eks fargate with load balancer
```
eksctl create cluster --name fargate-cluster-2 --region us-east-1 --zones=us-east-1a,us-east-1b,us-east-1d --fargate
```
```
eksctl create fargateprofile \
  --cluster fargate-cluster \
  --name parrot \
  --namespace parrot
```
```
eksctl get fargateprofile \
  --cluster fargate-cluster \
  -o yaml
```
```
- name: parrot
  podExecutionRoleARN: arn:aws:iam::949860833023:role/eksctl-fargate-cluster-clu-FargatePodExecutionRole-16XLVM0XW0KHG
  selectors:
  - namespace: parrot
  status: CREATING
  subnets:
  - subnet-03acbce539ad50732
  - subnet-07b8b1344ebd289db
```
```
eksctl utils associate-iam-oidc-provider \
    --region ${AWS_REGION} \
    --cluster fargate-cluster \
    --approve
2022-08-05 10:59:46 [ℹ]  will create IAM Open ID Connect provider for cluster "fargate-cluster" in "us-east-1"
2022-08-05 10:59:48 [✔]  created IAM Open ID Connect provider for cluster "fargate-cluster" in "us-east-1"
```
```
curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/install/iam_policy.json
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json
rm iam_policy.json
```
```
eksctl create iamserviceaccount \
  --cluster fargate-cluster  \
  --namespace kube-system \
  --name aws-load-balancer-controller2 \
  --attach-policy-arn arn:aws:iam::949860833023:policy/AWSLoadBalancerControllerIAMPolicy \
  --override-existing-serviceaccounts \
  --approve
```
```
kubectl get sa aws-load-balancer-controller2 -n kube-system -o yaml
```
```
kubectl apply -k "github.com/aws/eks-charts/stable/aws-load-balancer-controller/crds?ref=master"
```
```
helm repo add eks https://aws.github.io/eks-charts

export VPC_ID=$(aws eks describe-cluster \
                --name fargate-cluster \
                --query "cluster.resourcesVpcConfig.vpcId" \
                --output text)

helm upgrade -i aws-load-balancer-controller2 \
    eks/aws-load-balancer-controller2 \
    -n kube-system \
    --set clusterName=fargate-cluster \
    --set serviceAccount.create=false \
    --set serviceAccount.name=aws-load-balancer-controller \
    --set image.tag=1-0-0 \
    --set region=${AWS_REGION} \
    --set vpcId=${VPC_ID} \
    --version="${LBC_CHART_VERSION}"