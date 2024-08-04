# Aws-S3-Bucket-Policy-Exploration
## Project Description:
This project will guide you through creating a simple S3 bucket, defining a policy to manage access permissions, create IAM Users and Groups, assigning roles to each groups.

## Project Task:
1. Create an S3 Bucket
2. Understanding S3 Bucket Resource base Policies
3. Create IAM users and Groups
3. Policy Configuration 


## Step 1: Create an S3 bucket 
- Log in to the AWS Management Console 

![alt text](img/2.png)

- Navigate to the S3 service 

![alt text](img/3.png)

- Click the *"Create bucket"* button 

![alt text](img/4.png)

- Follow the prompts to configure your new S3 bucket ( maintain the default settings)

![alt text](img/5.png)

![alt text](img/7.png)

- You might get this prompt, S3 naming convention is unique (You can't have two bucket with same name in the whole of AWS infastructure)

- Add some extra characters or texts

![alt text](img/8.png)

![alt text](img/9.png)

## Step 2: Understanding S3 Bucket Policies [How Amazon S3 works with IAM]

### Scenario: As the cloud Architect, you're to 

###  Create IAM users, and assign them to different groups 
- Group 1 - Developers [Users - Gift, grace]
- Group 2 - Auditors [Ali, Josh]
- Group 3 - Operations [ Samuel, Lovet]

###  Assign different roles (policies) to each Groups

| Groups | Roles |
| ----------- | ----------- |
| Developers | EC2|
| Auditors | Billing and cost Management |
| Operation | Networking|

### Each Groups has a lead, assign a Resource-based policies within Amazon S3 only to the lead of each groups

### 2.1 Creating groups and assigning permissions 
- Navigate to IAM

![alt text](img/10.png)

- Select User groups

![alt text](img/11.png)

- Create groups

![alt text](img/12.png)

![alt text](img/13.png)

![alt text](img/14.png)

![alt text](img/15.png)

![alt text](img/16.png)


### Apply same Steps to create the other groups


- ### 2.2 Creating and Adding users 

![alt text](img/21.png)

![alt text](img/22.png)

![alt text](img/23.png)

![alt text](img/24.png)

![alt text](img/25.png)

### Apply same Steps to create the Users as you want 

![alt text](img/26.png)


### 2.3 Assign a Resource-based policies within Amazon S3 only to the lead of each groups

Assuming the leads are 

 Auditors - Ali 

 Developers - Gift 

 Operations - Samuel

 - Navigate to the bucket you created 

 ![alt text](img/27.png)

- Select Permission  

![alt text](img/28.png)

- Edit Bucket Policy

![alt text](img/29.png)

-  Copy this code 
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AddPublicReadCannedAcl",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::471112799800:user/Ali",
                    "arn:aws:iam::471112799800:user/samuel",
                    "arn:aws:iam::471112799800:user/grace"
                ]
            },
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl"
            ],
            "Resource": "arn:aws:s3:::bucketttesting/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "public-read"
                }
            }
        }
    ]
}
```

- Edit the principal, Copy the ARN URL of the users

![alt text](img/31.png)

- Edit the Resource, Copy the bucket ARN

![alt text](img/30d.png)

- You can edit the action, if you want 

![alt text](img/30g.png)

- Save Changes 

![alt text](img/30h.png)

### Alternatively 

- Use the policy generator 

![alt text](img/30.png)

- Select S3 Bucket policy

 ![alt text](img/30a.png)

 - Select Allow 

![alt text](img/30b.png)

- Select any action, you can select as many as you like 

![alt text](img/30c.png)

- Copy the bucket ARN 

![alt text](img/30e.png)

- Select Generate Policy

![alt text](img/30f.png)







