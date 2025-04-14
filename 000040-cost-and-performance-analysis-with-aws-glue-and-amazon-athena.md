# Cost and performance analysis with AWS Glue and Amazon Athena

See the workshop at <https://000040.awsstudygroup.com/>

## 1. Introducing AWS Glue & Amazon Athena

## 2. Preparation

### 2.1 Preparing the database

### 2.2 Building a database

> [!WARNING]
> In my case, to have the table `monthly_report`, I need to choose the AWS Glue crawler's **data source** of `s3://my-fcj-cost-and-usage-analysis-bucket/Monthly-Report/`.
>
> If I choose the data source of `s3://my-fcj-cost-and-usage-analysis-bucket/`, the table would have the name of the S3 bucket (`my-fcj-cost-and-usage-analysis-bucket`)

### 2.3 Database Check

## 3. Analysis of cost and usage performance

### 3.1 Data in the Table

### 3.2 Cost

### 3.3 Tagging and Cost Allocation

### 3.4 Usage

## 4. Clean up resources

> [!TIP]
> Remember to delete the IAM Role created for your AWS Glue **Crawler**.

> [!TIP]
> Unset `Query result location` of Amazon Athena.
