# LADV: Advanced Design Patterns for Amazon DynamoDB

See the workshop at

- <https://000039.awsstudygroup.com/3-ladv/>
- or <https://catalog.workshops.aws/dynamodb-labs/en-US/design-patterns>

## 1. Start here: Getting Started

### 1.1. Getting Started

### 1.2. Step 1 - Open the AWS Systems Manager Console

### 1.3. Step 2 - Check the Python and AWS CLI installation

### 1.4. Step 3 - Check `boto3` installation

### 1.5. Step 4 - Check the content of the workshop folder

### 1.6. Step 5 - Check the files format and content

### 1.7. Step 6 - Preload the items for the table Scan exercise

## 2. Exercise 1: DynamoDB Capacity Units and Partitioning

### 2.1. Step 1 - Create the DynamoDB table

### 2.2. Step 2 - Load sample data into the table

### 2.3. Step 3 - Load a larger file to compare the execution times

### 2.4. Step 4 - View the CloudWatch metrics on your table

### 2.5. Step 5 - Increase the capacity of the table

### 2.6. Step 6 - After increasing the table’s capacity, load more data

### 2.7. Step 7 - Create a new table with a low-capacity global secondary index

## 3. Exercise 2: Sequential and Parallel Table Scans

### 3.1. Step 1 - Execute a sequential Scan

### 3.2. Step 2 - Execute a parallel Scan

## 4. Exercise 3: Global Secondary Index Write Sharding

### 4.1. Step 1 - Creating the GSI

### 4.2. Step 2 - Querying the GSI with shards

## 5. Exercise 4: Global Secondary Index Key Overloading

### 5.1. Step 1 - Create the employees table for global secondary index key overloading

### 5.3. Step 3 - Query the employees table using the global secondary index with overloaded attributes

### 5.2. Step 2 - Load data into the new table

## 6. Exercise 5: Sparse Global Secondary Indexes

### 6.1. Step 1 - Add a new global secondary index to the employees table

### 6.2. Step 2 - Scan the employees table to find managers without using the sparse global secondary index

### 6.3. Step 3 - Scan the employees table to find managers by using the sparse global secondary index

## 7. Exercise 6: Composite Keys

### 7.1. Step 1 - Create a new global secondary index for City-Department

### 7.2. Step 2 - Query all the employees from a state

### 7.3. Step 3 - Query all the employees of a city

### 7.4. Step 4 - Querying all the employees of a city and a specific department

## 8. Exercise 7: Adjacency Lists

### 8.1. Step 1 - Create and load the the `InvoiceAndBills` table

### 8.2. Step 2 - Review the `InvoiceAndBills` table on the DynamoDB console

### 8.3. Step 3 - Query the table's invoice details

### 8.4. Step 4 - Query the Customer details and Bill details using the Index

## 9. Exercise 8: Amazon DynamoDB Streams and AWS Lambda

### 9.1. Step 1 - Create the replica table

### 9.2. Step 2 - Review the AWS IAM policy for the IAM role

### 9.3. Step 3 - Create the Lambda function

### 9.4. Step 4 - Enable DynamoDB Streams

### 9.5. Step 5 - Map the source stream to the Lambda function

### 9.6. Step 6 - Populate the `logfile` table and verify replication to `logfile_replica`
