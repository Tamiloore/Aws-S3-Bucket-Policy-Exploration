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

![2](https://github.com/user-attachments/assets/7515410d-19cd-4e24-a2ae-14144b295a6d)


- Navigate to the S3 service 

![3](https://github.com/user-attachments/assets/9dcaa4c7-de71-4cc3-b831-b47445a881d2)


- Click the *"Create bucket"* button 

![4](https://github.com/user-attachments/assets/31a716f3-5b4f-4328-869e-ee72088597de)


- Follow the prompts to configure your new S3 bucket ( maintain the default settings)

![5](https://github.com/user-attachments/assets/7021f9b6-8d98-4be6-84dd-77db62827d7b)


![7](https://github.com/user-attachments/assets/83da1c62-3417-4811-9253-12eae1ffc028)


- You might get this prompt, S3 naming convention is unique (You can't have two bucket with same name in the whole of AWS infastructure)

- Add some extra characters or texts

![8](https://github.com/user-attachments/assets/dfc0acda-6509-42a6-8a36-0f941f3ab8c2)


![9](https://github.com/user-attachments/assets/e1619ba3-ab45-46a5-800e-4c966816924e)


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

![10](https://github.com/user-attachments/assets/c4e704c1-e074-46da-9f21-f750cd54f456)


- Select User groups

![11](https://github.com/user-attachments/assets/d47c5b03-3795-45b9-b345-8c0a5465f135)


- Create groups

![12](https://github.com/user-attachments/assets/5e23d6e5-526a-469d-9858-e07e7ca151ac)


![13](https://github.com/user-attachments/assets/2cf00f24-9e1d-4227-89f0-47c7ed8cebac)


![14](https://github.com/user-attachments/assets/715c8e0c-062b-40e3-b778-c3c41b00a3e6)


![15](https://github.com/user-attachments/assets/d4ef2f7f-4b98-46df-8fa3-7814bdd60ab1)


![16](https://github.com/user-attachments/assets/81ac7d71-f0d6-4363-9886-ec660f75809e)


### Apply same Steps to create the other groups


- ### 2.2 Creating and Adding users 

![21](https://github.com/user-attachments/assets/f3df1df1-72fb-4bc0-bbb4-f19912f0b177)


![22](https://github.com/user-attachments/assets/ae8183b2-529f-4003-a0a8-46f1261bc602)


![23](https://github.com/user-attachments/assets/0d8dbe92-bb5a-4d3c-b031-b59503d25177)


![24](https://github.com/user-attachments/assets/65244606-869c-4cb7-be43-f31f925d6ac4)


![25](https://github.com/user-attachments/assets/701dcae9-1ce4-4deb-b286-c5bed5a530cf)


### Apply same Steps to create the Users as you want 

![26](https://github.com/user-attachments/assets/1fd93355-732b-4da6-8fea-c5062f8b670f)



### 2.3 Assign a Resource-based policies within Amazon S3 only to the lead of each groups

Assuming the leads are 

 Auditors - Ali 

 Developers - Gift 

 Operations - Samuel

 - Navigate to the bucket you created 

![27](https://github.com/user-attachments/assets/73de8db5-1087-49cb-9a74-7e6d778de413)


- Select Permission  

![28](https://github.com/user-attachments/assets/5dbeb545-5ee0-45f0-abe0-ff5cecfa08e5)


- Edit Bucket Policy

![29](https://github.com/user-attachments/assets/f3df2d99-4acd-4163-9b74-583b824e2f18)


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
  
![31](https://github.com/user-attachments/assets/23738d1e-b208-421d-80d1-8c9ee374dcbd)


- Edit the Resource, Copy the bucket ARN



- You can edit the action, if you want 

![30g](https://github.com/user-attachments/assets/58f50a18-7173-4f94-b234-a4c222c673cc)


- Save Changes 

![30h](https://github.com/user-attachments/assets/6cb717c3-29aa-40fe-ab4c-05294686da1f)


### Alternatively 

- Use the policy generator 

![30](https://github.com/user-attachments/assets/8404c122-ce34-4793-8f83-2018d8e7b5af)


- Select S3 Bucket policy

 ![30a](https://github.com/user-attachments/assets/e58d7f47-1a8f-467b-9e7a-b449882737f5)


 - Select Allow 

![30b](https://github.com/user-attachments/assets/25f77f43-c411-4fba-af66-a06e52dc465e)


- Select any action, you can select as many as you like 

![30c](https://github.com/user-attachments/assets/c552a2ba-f9e8-4bbe-96de-9be6250d84ff)


- Copy the bucket ARN 

![30e](https://github.com/user-attachments/assets/4398ea39-a401-4b9d-abd9-0ac44ee91beb)


- Select Generate Policy

![30f](https://github.com/user-attachments/assets/5e073406-3b01-426e-a087-7dc13507dfd9)








