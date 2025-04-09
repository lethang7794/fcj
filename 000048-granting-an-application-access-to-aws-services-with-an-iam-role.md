# Granting an Application access to AWS services with an IAM role

See the workshop at <https://000048.awsstudygroup.com/>

## 1. Preparation

### 1.1 Create EC2 Instance

### 1.2 Create S3 bucket

## 2. Use access key

### 2.1 Generate IAM user and access key

### 2.2 Use access key

- Create a file named `test.txt`:

  ```bash
  tee test.txt <<EOF
  This a the first file
  EOF
  ```

- Write a Python script to upload a file to S3 using access key:

  ```bash
  tee upload-s3-using-access-key.py <<EOF
  import boto3

  # AWS credentials
  ACCESS_KEY = "<FILL_IN_ACCESS_KEY>"
  SECRET_ACCESS_KEY = "<FILL_IN_SECRET_ACCESS_KEY>"
  S3_BUCKET_NAME = "<FILL_IN_S3_BUCKET_NAME>"

  UPLOAD_FILE="test.txt"
  UPLOAD_PATH="test.txt"

  # Initialize S3 client
  s3 = boto3.client(
      "s3", aws_access_key_id=ACCESS_KEY, aws_secret_access_key=SECRET_ACCESS_KEY
  )

  # Upload file to S3
  s3.upload_file(UPLOAD_FILE, S3_BUCKET_NAME, UPLOAD_PATH)
  EOF
  ```

- Run the script:

  ```bash
  python3 upload-s3-using-access-key.py
  ```

> [!TIP]
> If your EC2 instance is using
>
> - Amazon Linux 2023, run the Python script with Python 3 (`python3` (AL2023 removed Python 2.7[^1]))
> - Amazon Linux 2, run the Python script with Python 2 (`python`)

## 3. IAM role on EC2

### 3.1 Create IAM role

### 3.2 Using IAM role

- Create a file named `test-2.txt`:

  ```bash
  tee test-2.txt <<EOF
  This a the second file
  EOF
  ```

- Write a Python script to upload a file to S3 using access key:

  ```bash
  tee upload-s3-using-role.py <<EOF
  import boto3

  S3_BUCKET_NAME = "<FILL_IN_S3_BUCKET_NAME>"
  UPLOAD_FILE="test-2.txt"
  UPLOAD_PATH="test-2.txt"

  # Initialize S3 client
  s3 = boto3.client("s3")

  # Upload file to S3
  s3.upload_file(UPLOAD_FILE, S3_BUCKET_NAME, UPLOAD_PATH)
  EOF
  ```

- Run the script:

  ```bash
  python3 upload-s3-using-role.py
  ```

> [!NOTE]
> If your instance is using `Amazon Linux 2023` AMI, checking credential of the instance profile is a little different:
>
> ```bash
> TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`
> curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/iam/security-credentials/ec2roles3upload
> ```
>
> (`Amazon Linux 2023` use IMDSv2, so you need to use `curl` to get the token first.[^2])

## 4. Clean up resources

> [!TIP]
> Don't forget to delete the security group too.

[^1]: <https://docs.aws.amazon.com/linux/al2023/ug/python.html>
[^2]: <https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html>

---
