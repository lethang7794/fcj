# IAM Role & Condition

## 1. Introduction about IAM

> [!NOTE]
> How IAM works?
>
> ---
>
> IAM (_Identity_ and **Access** Management) provides the infrastructure necessary to control _authentication_ and **authorization** for your AWS account.
>
> ![How IAM works](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/intro-diagram%20_policies_800.png)
>
> - (1) First, a human user or an application uses their sign-in **credentials** to authenticate with AWS.
>
>   - IAM
>     - (2) matches the sign-in credentials to a **principal** (an IAM user, federated user, IAM role, or application) trusted by the AWS account -
>     - (3) _authenticates_ permission to access AWS.
>
> - (4) When a principal tries to use the AWS Management Console, the AWS API, or the AWS CLI, (5) that principal _sends a request_ to AWS.
>
>   - (6) AWS gathers the request information into a **_request context_**, that includes:
>
>     - Principal
>     - Action
>     - Resources
>     - Resource data: e.g. EC2 instance ID, DynamoDB table name...
>     - Environment data: e.g. IP address
>
>   - (7) IAM evaluates the _request context_ to authorize the request.
>
> - Next, IAM makes a request to _grant_ the principal **access** to resources.
>
>   - IAM grants or denies access in response to an **authorization request**.
>   - For example:
>
>     - When you first sign in to the console and are on the console Home page, you aren't accessing a specific service.
>     - When you select a service,
>
>       - you send an authorization request to IAM for that service.
>       - IAM verifies that your identity is on the list of authorized users, determines what policies control the level of access granted, and evaluates any other policies that might be in effect.
>
>       Principals within your AWS account or from another AWS account that you trust can make authorization requests.
>
> - Once authorized, the **principal** can _perform **actions**_ on **resources** in your AWS account.
>
>   - For example, the principal could launch a new Amazon Elastic Compute Cloud instance, modify IAM group membership, or delete Amazon Simple Storage Service buckets.
>
> For more details, see [How IAM works](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

### 1.1 Request to AWS service

### 1.2 Authenticate requests

> [!NOTE]
> To send a request to AWS, a principal must first authenticate with AWS (sign-in) via credentials.
>
> Depends on the type of principal, the credentials can be different.
>
> - For **human users**, the credentials are the sign-in credentials.
>   - For root user, it's the root user's email address and password.
>   - For IAM user, it's AWS account ID/alias, IAM username and password.
>   - For users in an AWS IAM Identity Center, it's the IAM Identity Center user name and password.
> - For **applications**, the credentials are the access keys.
> - For **AWS services**, the recommend credentials are the temporary security credentials from AWS STS service.

### 1.3 Assume Role Process

> [!NOTE]
> To assume a role:
>
> - the principal must have _**permission** to assume_ the role.
>
>   - For example, the principal is an IAM user `UserA` and the policy attached to `UserA` allows it to assume `RoleA`.
>
>     ```json
>     {
>       "Version": "2012-10-17",
>       "Statement": {
>         "Effect": "Allow",
>         "Action": "sts:AssumeRole",
>         "Resource": "arn:aws:iam::<ACCOUNT-ID>:role/RoleA"
>       }
>     }
>     ```
>
> - the role must have a _trust policy_ that allows the principal to assume it.
>
>   - For example, the role `RoleA` can have a trust policy that
>
>     - Allows the root user to assume the role.
>
>       ```json
>       {
>         "Version": "2012-10-17",
>         "Statement": [
>           {
>             "Effect": "Allow",
>             "Principal": { "AWS": "arn:aws:iam::<ACCOUNT-ID>:root" },
>             "Action": "sts:AssumeRole"
>           }
>         ]
>       }
>       ```
>
>     - Allows the IAM user `UserA` to assume the role.
>
>       ```json
>       {
>         "Version": "2012-10-17",
>         "Statement": [
>           {
>             "Effect": "Allow",
>             "Principal": { "AWS": "arn:aws:iam::<ACCOUNT-ID>:user/UserA" },
>             "Action": "sts:AssumeRole"
>           }
>         ]
>       }
>       ```
>
> For more information, see:
>
> - [Switch from a user to an IAM role (console) - AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-console.html)
> - [Create a role to give permissions to an IAM user - AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html)
> - [Grant a user permissions to switch roles - AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_permissions-to-switch.html)
> - [AWS JSON policy elements: Principal - AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-roles)
>   - [AWS account principals](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-accounts)
>   - [IAM user principals](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-users)

## 2. Create IAM Group

## 3. Create IAM User

### 3.1 Create IAM Users

### 3.2 Check permissions

## 4. Configure Role Condition

### 4.1 Create Admin IAM Role

> [!TIP]
> AWS IAM's Create Role Wizard now supports creating a role with `Custom trust policy`.
>
> - Choose `Custom trust policy`.
> - Choose the placeholder statement `Statement1`.
> - In the `Add a principal` section, choose `Add`.
> - In the `Add Principal` dialog, choose `Principal type` of `IAM users`.
> - Replace `{Account}` and `{UserName}` placeholders with your AWS account ID and IAM user name.

### 4.2 Configure Switch role

### 4.3 Restrict role access

#### 4.3.1 Limit switch role by IP

> [!TIP]
> To know your IP address, you can
>
> - open <https://checkip.amazonaws.com/> in your browser.
> - use the following command:
>
>   ```bash
>   curl -s https://checkip.amazonaws.com
>   ```

> [!NOTE]
> See [AWS global condition context key](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) > [!NOTE]
> See [AWS global condition context key](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html)
>
> - [Properties of the network](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-network-properties)
>   - [aws:SourceIp](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceip)
>   - [aws:SourceVpc](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcevpc)
>   - [aws:SourceVpce](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcevpce)
>   - [aws:VpcSourceIp](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-vpcsourceip)

#### 4.3.2 Limit switch role by Time

> [!NOTE]
> See [AWS global condition context key](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html)
>
> - [Properties of the request](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-request-properties)
>
>   - [aws:CurrentTime](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-currenttime)
>   - [aws:RequestedRegion](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-requestedregion)
>   - [aws:RequestTag/tag-key](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-requesttag)
>   - [aws:TagKeys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-tagkeys)
>   - [aws:SecureTransport](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-securetransport)
>   - [aws:SourceAccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount)
>   - [aws:SourceArn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn)
>   - ...

## 5. Clean up resources
