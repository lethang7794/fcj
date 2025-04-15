# Work with Amazon DynamoDB

See the workshop at <https://000060.awsstudygroup.com/>

## 1. Introduction

### 1.1 Core Components of Amazon DynamoDB

| Relational Database, e.g. Postgres, MySQL | DynamoDB                                                                                  | Note                                          |
| ----------------------------------------- | ----------------------------------------------------------------------------------------- | --------------------------------------------- |
| ~ Table                                   | Table                                                                                     |                                               |
| ~ Row                                     | Item                                                                                      |                                               |
| ~ Column                                  | Attribute                                                                                 |                                               |
|                                           |                                                                                           |                                               |
| ~ Primary Key                             | Partition Key                                                                             |                                               |
| ~ Primary Key                             | Partition Key + Sort Key (aka Composite Primary Key)                                      |                                               |
|                                           |                                                                                           |                                               |
| ~ Index                                   | **Local** Secondary Index (LSI):          ***Same* partition** key + *Different sort* key | Each DynamoDB table has a maximum of  5 LSIs. |
|                                           | **Global** Secondary Index (GSI): ***Different* partition** key + *Different sort* key    | Each DynamoDB table has a maximum of 20 GSIs. |

### 1.2 Primary Key

### 1.3 Secondary Index

### 1.4 Naming Rules and Data Types

### 1.5 Read Consistency

### 1.6 Read/Write Capacity Mode

## 2. Preparation

### 2.1 Manage using AWS Management Console

#### 2.1.1 Create access key

> [!TIP]
> This step is for [3.1 Configure AWS CLI](#31-configure-aws-cli), you can do it later.

#### 2.1.2 Create a table

#### 2.1.3 Write data

#### 2.1.4 Read data

#### 2.1.5 Update data

#### 2.1.6 Query data

#### 2.1.7 Create a Global Secondary Index

#### 2.1.8 Query the Global Secondary Index

### 2.2 Use AWS CloudShell

> [!TIP]
> You can use AWS CloudShell, or your own shell/terminal on your local machine.

#### 2.2.1 Create a table

> [!WARNING]
> The `- provided-throughput` option of `aws dynamodb create-table` has been changed to `--provisioned-throughput`

> [!TIP]
> The updated command should be
>
> ```shell
> aws dynamodb create-table \
>    --table-name Music \
>    --attribute-definitions \
>        AttributeName=Artist,AttributeType=S \
>        AttributeName=SongTitle,AttributeType=S \
>    --key-schema \
>        AttributeName=Artist,KeyType=HASH \
>        AttributeName=SongTitle,KeyType=RANGE \
>    --provisioned-throughput \
>        ReadCapacityUnits=10,WriteCapacityUnits=5 \
>    --table-class STANDARD
> ```

> [!TIP]
> With DynamoDB, you can create multiple tables with the _same_ name in _different_ AWS regions.

#### 2.2.2 Write data

> [!NOTE]
> In DynamoDB, attribute name can include spaces.
>
> - The followings `aws dynamodb put-item` commands:
>
>   ```shell
>   aws dynamodb put-item \
>       --table-name Music \
>       --item \
>           '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Call Me Today"}, "AlbumTitle": {"S": "Somewhat Famous"}, "Awards": {"N": "1"}}'
>
>   aws dynamodb put-item \
>       --table-name Music \
>       --item \
>           '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Howdy"}, "AlbumTitle": {"S": "Somewhat Famous"}, "Awards ": {"N": "2"}}'
>   ```
>
>   will create items with 2 different attributes:
>
>   - `Awards` (without a space) and
>   - `Awards ` (with a trailing space)

> [!IMPORTANT]
> DynamoDB is a key-value NoSQL database which allows flexible schema.
>
> The flexible schema can be demonstrated by previous "mistake":
>
> - You can create an item with `Awards` attribute or `Awards ` attribute without pre-defined the schema.
>
> This is known as _schema-on-read_, the schema isn't enforced at writing as of RDBM (which is known as _schema-on-write_).

#### 2.2.3 Read data

#### 2.2.4 Update data

> [!IMPORTANT]
>  *Expression attribute values* in Amazon DynamoDB act as variables.
>
> - They're substitutes for the **actual values** that you want to compare — values that you might _not know until runtime_.
> - An expression attribute value must begin with a colon (`:`) and be followed by one or more alphanumeric characters.
>
> See [Using expression attribute values in DynamoDB - Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ExpressionAttributeValues.html)

> [!TIP]
> In the lab, the command after formatted looks like this:

```shell
aws dynamodb update-item \
     --table-name Music \
     --key '{ "Artist": {"S": "Acme Band"}, "SongTitle": {"S": "Happy Day"}}' \
     --update-expression "SET AlbumTitle = :newval" \
     --expression-attribute-values '{ ":newval": { "S": "Album Title v3" } }' \
     --return-values ALL_NEW
```

- At runtime, the `:newval` in `--update-expression "SET AlbumTitle = :newval"` will be substituted for the value `{ "S": "Updated Album Title" }`


#### 2.2.5 Query data

> [!WARNING]
> There are 2 extra zero space characters after `--expression-attribute-values`, which make the command unparsable.
>
> ```shell
> aws dynamodb query \
>     --table-name Music \
>     --key-condition-expression "Artist = :name" \
>     --expression-attribute-values <200b><200b>'{":name":{"S":"Acme Band"}}'
>
>
> Error parsing parameter '--expression-attribute-values': Expected: '=', received: '​' for input:
>  ​​{":name":{"S":"Acme Band"}}
> ^
> ```

> [!TIP]
> The correct command should be as following:
>
> ```shell
> aws dynamodb query \
>     --table-name Music \
>     --key-condition-expression "Artist = :name" \
>     --expression-attribute-values '{":name":{"S":"Acme Band"}}'
> ```

#### 2.2.6 Create Global Secondary Index

#### 2.2.7 Query Global Secondary Index

> [!WARNING]
> There are 2 extra zero space characters make the command unparsable:
>
> ```shell
> aws dynamodb query \
>     --table-name Music \
>     --index-name AlbumTitle-index \
>     --key-condition-expression "AlbumTitle = :name" \
>     --expression-attribute-values <200b><200b>'{":name":{"S":"Somewhat Famous"}}'
> ```
>
> The correct command should be as following:
>
> ```shell
> aws dynamodb query \
>     --table-name Music \
>     --index-name AlbumTitle-index \
>     --key-condition-expression "AlbumTitle = :name" \
>     --expression-attribute-values '{":name":{"S":"Somewhat Famous"}}'
> ```

## 3. Begin with AWS SDK

### 3.1 Configure AWS CLI

### 3.2 Getting started with Python and DynamoDB

#### 3.2.1 Create table

#### 3.2.2 Write data

#### 3.2.3 Read data

#### 3.2.4 Update data

#### 3.2.5 Delete data

#### 3.2.6 Load sample data

#### 3.2.7 Query data

#### 3.2.8 Scan data

#### 3.2.9 Delete the table

## 4. Clean up resource
