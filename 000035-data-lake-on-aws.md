# Data Lake on AWS

See the workshop at <https://000035.awsstudygroup.com/>

## 1. Introduction

## 2. Preparation Steps

### 2.1 Creating an IAM Role

### 2.2 Create Policy

## 3. Data Collection and Storage

### 3.1 Create S3 Bucket

> [!TIP]
> You will need the name of the S3 bucket later in [step 5](#5-data-transformation)

### 3.2 Creating a Delivery Stream

> [!IMPORTANT]
> The Management UI of Kinesis service has been updated:
>
> - A ~~_delivery stream_~~ is now a _Firehose stream_.
> - ~~_Amazon **Kinesis Data Firehose**_~~ service is now _Amazon **Data Firehose**_ service.

> [!TIP]
> To create a _Firehose stream_ (formerly _Delivery stream_):
>
> - Open the _Data Firehose_ service:
>   - Directly via [this link](https://console.aws.amazon.com/firehose/home)
>   - or via the search UI with the value `Amazon Data Firehose`
>   - or as a link in Kinesis service's navigation drawer.
> - Open _Firehose stream_ in navigation drawer.
> - Click `Create Firehose stream`

> [!NOTE]
> By default, Amazon Data Firehose appends the prefix `YYYY/MM/dd/HH` (in UTC) to the data it delivers to Amazon S3.
>
> In this workshop, by configure the delivery stream's _Destination settings_ / _S3 bucket prefix_ to `data/raw/`
>
> NOTE: the slash `/` after `raw` is important. If you miss it Firehose will copy the data into an undesired location.

> [!WARNING]
> In the workshop, S3 bucket prefix is configured to `data/raw`, which cause the data to copy to undesired location.
>
> e.g.
>
> - If you do the workshop in 2022, the data will be copy to `data/raw2022` directory.
> - If you do the workshop in 2025, the data will be copy to `data/raw2025` directory.

### 3.3 Create Sample Data

> [!NOTE]
> The CloudFormation template in the workshop (the **cognito-setup.json** file from [First Cloud Journey](https://raw.githubusercontent.com/AWS-First-Cloud-Journey/Lab-000035-DataLake-on-AWS/master/cognito-setup.json)) is outdated.
>
> - If you create a CloudFormation stack from that template, you will encounter an error like this:
>
>   ```
>   The following resources failed to deploy:
>   Resource Name: LambdaExecutionRole (AWS::IAM::Role)
>   Event Type: create
>   Reason: Resource handler returned message: "A condition block must be present for the Cognito provider (Service: Iam, Status Code: 400, Request ID: a7c1f84f-53f9-450b-ab6b-61c20a0b590a)" (RequestToken: 91410630-55e8-cdb6-fa49-00c9bc9ede63, HandlerErrorCode: InvalidRequest)
>   ```
>
> To resolve this problem, you can:
>
> - Fix the template yourself as in [this commit](https://github.com/awslabs/amazon-kinesis-data-generator/commit/a9839a379699ad2649a8e0e6e4d8ee338bdceabb) of [awslabs](https://github.com/awslabs)/**[amazon-kinesis-data-generator](https://github.com/awslabs/amazon-kinesis-data-generator)** repo.
> - Or use the updated template from [this link](https://github.com/awslabs/amazon-kinesis-data-generator/blob/mainline/setup/cognito-setup.yaml) (_Click_ `Raw` then _right click_ and _choose_ `Save as`)

## 4. Create Data Catalog

### 4.1 Create Glue Crawler

> [!TIP]
> When creating a AWS Glue _Crawler_,
>
> - In `Step 2 - Choose data sources and classifiers` / `Add a data source` / `Subsequent crawler runs`, choose `Crawl all sub-folders` so you can re-run the crawler for new folders.
> - In `Step 3 - Configure security settings` / `IAM role`, choose the role created in [**2.1** Creating an IAM Role](https://000035.awsstudygroup.com/2-prerequiste/2.1-createiamrole/)

### 4.2 Data Check

## 5. Data Transformation

> [!TIP]
> In AWS Glue Studio, when creating the new notebook, you should use the existing notebook from the workshop.
>
> After download the existing notebook from the [workshop repo](https://github.com/AWS-First-Cloud-Journey/Lab-000035-DataLake-on-AWS/) - before upload to AWS Glue Studio - don't forget to :
>
> - change `yourname-datalake-demo-bucket` to your bucket name.

> [!NOTE]
> After run the notebook (as a job run), the processed data will be save to your S3 bucket at `data/processed_data`, re-run your AWS Glue _crawler_, so it's showed in your AWS Glue _Data Catalog_.

## 6. Analysis and visualization

### 6.1 Analysis with Athena

> [!NOTE]
> When execute the Athena query,
>
> ```SQL
> SELECT artist_name,
>        count(artist_name) AS count
> FROM processed_data
> GROUP BY artist_name
> ORDER BY count DESC
> ```

> you may end up with an error.
>
> Add the database `summitdb` to `FROM` clause as follow:
>
> ```SQL
> SELECT artist_name,
>        count(artist_name) AS count
> FROM summitdb.processed_data
> GROUP BY artist_name
> ORDER BY count DESC
> ```

### 6.2 Visualize with QuickSight

## 7. Clean up resources
