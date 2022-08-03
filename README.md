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

### Pricing tiers
- storage costs v accessibility, need to understand the balance between these 2 to get the best value
![](/images/s3_6.png)

### S3 Security and encyption
- bucket policies/access control list
- server side encryption on object
![](/images/s3_7.png)
- server side encryption on whole bucket
- every object uploaded will be encrypted because the bucket itself is encrypted
![](/images/s3_8.png)

### S3 Versioning
- Create a new bucket with the following settings
![](/images/s3_9.png)
- upload the hello.txt and modify the file and upload again
- in the bucket, enable `show versions` to see the previous versionss
![](/images/s3_10.png)
- delete the file, enable show versions,  the files should still appear in the list. The files should still be able to be opened
![](/images/s3_11.png)
- deleting the marker restores the files
- after permanently deleting the marker, the original file and its versions reappear
- versioning can only be suspended, new objects will not be versionsed, but any previous objects with versions will be preserved
![](/images/s3_12.png)
- each version can be deleted individually

### S3 lifecycle management
- go to version bucket > create lifecycle rule
![](/images/s3_13.png)
![](/images/s3_14.png)