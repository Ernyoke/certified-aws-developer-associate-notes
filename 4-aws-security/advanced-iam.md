# Advanced IAM

## Authorizaiton Model Evaluation of Policies

1. If there is an explicit DENY condition in the policy, end decision and DENY access
2. If there is an ALLOW condition, end decision with ALLOW access
3. Else DENY

- If there is both an explicit DENY and explicit ALLOW condition, DENY wins because it gets executed first

## IAM Policies and S3 Bucket Policies

- IAM Policies are attached to users, roles and groups
- S3 Bucket policies are attached to buckets
- When the evaluations happens, if an IAM Principal can perform an operation on a bucket, the union of its assigned IAM Policies and S3 Bucket Policies will be evaluated
- Example1:
    - IAM Role attached to EC2 instance, authorizes RW on "my_bucket"
    - No S3 Bucket Policy attached
    - EC2 instance can read and write to "my_bucket" because of the attached IAM Role
- Example2:
    - IAM Role attached to EC2 instance, authorizes RW on "my_bucket"
    - S3 Bucket Policy explicitly denies the access from the IAM Role
    - EC2 can not read adn write from the bucket, because explicit deny has higher priority then the expliced allow
- Example3:
    - IAM Role attached to EC2 instance, no S3 bucket permissions
    - S3 Bucket Policy explicitly allows RW to the IAM Role
    - EC2 instance can read and write to the bucket, union policy has the read write access

## Dynamic Policies with IAM

- How do we assign each user a `/home/<user>` folder in S3 bucket?
- Option 1:
    - Create policies for each user, everytime we create an user we create a policy (DOES NOT SCALE!)
- Option 2:
    - Create one dynamic policy with IAM
    - Leverage the special policy variable **${aws:username}**

## Inline and Managed Policies

### AWS Managed Policies

- Maintained by AWS
- Good for power users and administrators
- Updated by AWS in case of new services/new APIs

### Customer Managed Policies

- Created by AWS users, maintained by AWS users
- They are re-usable, can be applied to many principals
- They are version controlled, the can be rolled back, there is a central change management to see who did what
- They are best practice!

### Inline Policies

- Strict one-to-one relationship between policy and principal
- Policy is deleted when the IAM principal is deleted
- Policy max bytes it 2KB, we can not create policies larger than that

## Granting Users Permission to Pass a Role to an AWS Service

- To configure many AWS services, we must pass an IAM role to the service
- The service will later assume the role and perform the actions it needs to perform
- Example of passing a role:
    - We create a customer role and assign it to an EC2 instance
    - We create an IAM Role and pass it to a Lambda Function
- In order to be able to assign role to services we need the **iam:PassRole** permission
- It often comes with **iam:GetRole** permission to view the role being passed

## Can any role be passed to any service?

- **No**: roles can only be passed to what their **trust** allows
- A trust policy in case of a role is an indication to which service it can be granted
