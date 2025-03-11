# Data protection with AWS Backup

See the workshop at <https://000013.awsstudygroup.com/>

## 1. Introduction

## 2. Preparation

### 2.1 Create S3 Bucket

> [!TIP]
> The S3 bucket will be used to store
>
> - the CloudFormation stack template
> - the source code for lambda function used to validate that the backup can be restored

> [!TIP]
> There is an error in the example policy: `Resources` should be without `s`.

### 2.2 Deploy infrastructure

## 3. Create Backup plan

> [!TIP]
> The `Use backups window defaults - recommended` has been removed by AWS.

> [!WARNING]
> Instead of using CLI with access key, you should:
>
> - Use [AWS CloudShell], a browser-based CLI, to run commands. Learn more
> - Use the AWS CLI V2 and enable authentication through a user in IAM Identity Center. Learn more

## 4. Set up notifications

## 5. Test Restore

## 6. Clean up resources

> [!TIP]
> You should also cleanup the S3 bucket.

[AWS CloudShell]: https://console.aws.amazon.com/cloudshell
