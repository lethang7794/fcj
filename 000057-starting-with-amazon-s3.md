# STARTING WITH AMAZON S3

See the workshop at <https://000057.awsstudygroup.com/>

## 1. Introduction

## 2. Preparation

### 2.1 Create S3 bucket

### 2.2 Load data

## 3. Enable static website feature

## 4. Configuring public access block

## 5. Configuring public objects

> [!NOTE]
> The workshop use _ACL_ to make the objects public.
>
> See: [Managing access with ACLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acls.html)

> [!TIP]
> An other way to make objects public is using a _bucket policy_ (that grants public read access), which is now recommend by AWS.
>
> See: [Setting permissions for website access](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html)

## 6. Test website

## 7. Accelerate Static Websites with Cloudfront

### 7.1 Block all public access

> [!TIP]
> After turn `Block all public access` on again, you should also
>
> - revert the changes to ACLs
> - or - in case using bucket policy - delete the bucket policy that grants public read access

### 7.2 Config Amazon CloudFront

> [!WARNING]
> If your bucket's already has a bucket policy, CloudFront might fail to update the bucket permission.
>
> In that case:
>
> - you need to manually update the bucket policy
> - or you can delete the existing bucket policy, then edit the origin and select `Yes, update the bucket policy` once more time, then `Save changes`.

> [!NOTE]
> As the name suggest `Legacy access identities`, _origin access identity_ (OAI) is ... legacy.
>
> - The recommend way now is using _origin access control_ (OAC) settings.
>
> See [Restrict access to an Amazon Simple Storage Service origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html)

> [!TIP]
> Because the S3 bucket is used to host a website (`Static website hosting` is turn on), the bucket has a _website endpoint_, which can also be used as the origin for CloudFront distribution.
>
> See:
>
> - [Website endpoints | S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteEndpoints.html)
> - [Use CloudFront to serve a static website that’s hosted on Amazon S3](https://repost.aws/knowledge-center/cloudfront-serve-static-website)
> - [Key differences between a website endpoint and a REST API endpoint](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteEndpoints.html#WebsiteRestEndpointDiff).

> [!WARNING]
> If a bucket has `Static website hosting` turned on, you can use the bucket website endpoint - as an origin for a CloudFront distribution - without using OAI or OAC.
>
> - CloudFront console will let you select a bucket website endpoint even if the bucket's `Block all public access` is on, which means when you access the CloudFront distribution, it will be a `403 Forbidden` response.

### 7.3 Test Amazon Cloudfront

## 8. Bucket Versioning

## 9. Move objects

## 10. Replication Object multi Region

> [!NOTE]
> AWS S3 console now doesn't allow you to choose the region for a bucket when creating.
>
> - You need to change the region before creating the bucket.

> [!TIP]
> While creating replication rule, if you don't see the new bucket when choosing destination, refresh the `Create replication rule` page.

## 11. Clean up resources
