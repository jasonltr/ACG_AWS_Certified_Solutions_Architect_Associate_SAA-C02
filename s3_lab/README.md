## ACG_AWS_Certified_Solutions_Architect_Associate_SAA-C02

I will be documenting my process of the AWS Solutions Architect course from [Acloudguru](https://learn.acloud.guru/course/aws-certified-solutions-architect-associate/overview) here

All content is from acloudguru

Main topics to focus on are
- S3
- Route 53
- VPC

Try to document lab exercises to show proof of concepts

## S3
- Starts from slide 57, follow [.pdf](/1621966269571-AWS%20Certified%20Solutions%20Architect%20Associate%20SAA-C02%20NEW%20PDF_compressed.pdf)

### Exercise Create an S3 bucket

- Create a new bucket with unique name
![](/s3_lab/images/s3_1.png)
- Upload some files
![](/s3_lab/images/s3_2.png)
- Able to modify the storage class at the object OR bucket level
![](/s3_lab/images/s3_3.png)
- go to bucket > permissions > uncheck block public access
![](/s3_lab/images/s3_4.png)
- go to the object itself > Actions > share with presigned url > 1 minute > paste url onto browser to see the image
![](/s3_lab/images/s3_5.png)

### Pricing tiers
- storage costs v accessibility, need to understand the balance between these 2 to get the best value
![](/s3_lab/images/s3_6.png)

### S3 Security and encyption
- bucket policies/access control list
- server side encryption on object
![](/s3_lab/images/s3_7.png)
- server side encryption on whole bucket
- every object uploaded will be encrypted because the bucket itself is encrypted
![](/s3_lab/images/s3_8.png)

### S3 Versioning
- Create a new bucket with the following settings
![](/s3_lab/images/s3_9.png)
- upload the hello.txt and modify the file and upload again
- in the bucket, enable `show versions` to see the previous versionss
![](/s3_lab/images/s3_10.png)
- delete the file, enable show versions,  the files should still appear in the list. The files should still be able to be opened
![](/s3_lab/images/s3_11.png)
- deleting the marker restores the files
- after permanently deleting the marker, the original file and its versions reappear
- versioning can only be suspended, new objects will not be versionsed, but any previous objects with versions will be preserved
![](/s3_lab/images/s3_12.png)
- each version can be deleted individually

### S3 lifecycle management
- go to version bucket > create lifecycle rule
![](/s3_lab/images/s3_13.png)
![](/s3_lab/images/s3_14.png)
- can play around with the lifecycle rules to manage the movement of files for accessibility/storage/cost reasons
- again need to study the use case to get the best value out of the lifecycle rules

### Sharing s3 buckets across accounts (need 2 aws accounts)
- cross account IAM roles. Programmatic AND console access
- IAM > create new role > ec2 > s3, select s3fullaccess
- The created role will have full access to s3 services only `S3_Cross_Account_Access`
- Add user > give a username and pw > create group > get link to login
![](/s3_lab/images/s3_15.png)
- Basically account 2 will have a role assigned to them by account 1, and account 2 will have admin rights to account 1's s3 services 

### Cross replication of s3 bucket across regions
- create a destination bucket2, objects uploaded to bucket1 will be replicated in bucket2
![](/s3_lab/images/s3_16.png)
- go to bucket1 > management > replication rules > create replication rule
![](/s3_lab/images/s3_17.png)
![](/s3_lab/images/s3_18.png)
- results in bucket2, took some time, but files are replicated
![](/s3_lab/images/s3_19.png)