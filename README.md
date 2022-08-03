## ACG_AWS_Certified_Solutions_Architect_Associate_SAA-C02

I will be documenting my process of the AWS Solutions Architect course from [Acloudguru](https://learn.acloud.guru/course/aws-certified-solutions-architect-associate/overview) here

All content is from acloudguru

Main topics to focus on are
- S3
- Route 53
- VPC

Try to document lab exercises to show proof of concepts

## S3
- Starts from slide 57, follow the [.txt](/S3%20101.txt) and [.pdf](/1621966269571-AWS%20Certified%20Solutions%20Architect%20Associate%20SAA-C02%20NEW%20PDF_compressed.pdf)

### Exercise Create an S3 bucket

- Create a new bucket with unique name
![](/images/s3_1.png)
- Upload some files
![](/images/s3_2.png)
- Able to modify the storage class at the object OR bucket level
![](/images/s3_3.png)
- go to bucket > permissions > uncheck block public access
![](/images/s3_4.png)
- go to the object itself > Actions > share with presigned url > 1 minute > paste url onto browser to see the image
![](/images/s3_5.png)