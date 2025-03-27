# S3 Encryption at rest with AWS KMS

## 1. Introduction

## 2. Preparation steps

### 2.1 Create Policy and Role

### 2.2 Create Group and User

## 3. Create Key Management Service

> [!NOTE]
> No AWS principal, including the account root user or key creator, has any permissions to a KMS key unless they are
>
> - explicitly allowed (by the KMS key's _key policy_), and
> - never denied, in a key policy, IAM policy, or grant.
>
> See: [AWS KMS Key Policies](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html)

> [!TIP]
> For better security, you can use 2 different roles with different permissions for the KMS key:
>
> - One for the **key administrator** who manages the key (create key, update key, delete key...)
> - One for the **key users** who use the key (encrypt, decrypt...)
>
> See: [AWS KMS Key Policies](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html)

## 4. Create Amazon S3

### 4.1 Create Bucket

### 4.2 Upload data to S3

## 5. Create AWS CloudTrail and Amazon Athena

### 5.1 Create CloudTrail

### 5.2 Logging to CloudTrail

### 5.3 Create Amazon Athena

### 5.4 Retrieve data with Athena

## 6. Test and share encrypted data on S3

## 7. Resource cleanup

> [!TIP]
> This workshop has the most detailed steps for cleaning resources. 👏

> [!WARNING]
> Don't forget to delete the Athena table.
