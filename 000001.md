# Creating your first AWS account

See the workshop at <https://000001.awsstudygroup.com>

## Overview

- Create an _AWS account_[^2] (that comes with a _root user_[^3])
  - Select Plan for AWS Support[^7].
- Setup MFA[^4]
- Use _IAM user_[^5] and _IAM user **group**_[^6] to manage access
  - The `AdminGroup` IAM group[^8]
  - The `AdminUser` IAM user

## 1. Create new AWS account

### Create an AWS account

### Add payment method

- My VietinBank card is not accepted, I need to use a Vietcombank card.

### Verify your phone number

- The OTP is delivery via a phone call, not a SMS.

### Select Support Plan

### Wait for your account to be activated

> [!CAUTION]
> Do not provide your AWS credentials (username/password or access keys) to anybody, or they can do "anything" with your account.

## 2. MFA for AWS Accounts

You can use 3 type of MFA devices:

- Virtual MFA (Authenticator app), e.g. 2FAS (I use this)
- Security Key or Passkey
- Hardware TOTP token

> [!TIP]
> Use Passkey for a better UX.

## 3. Create Admin Group and Admin User

### Create `AdminGroup`

### Create `AdminUser` (in `AdminGroup`)

### Login to `AdminUser`

## 4. Account Authentication Support

## 5. Explore and Configure AWS Management Console

### Choose your Region

- For most services, you can choose an AWS Region that specifies where your resources are managed
- For some services, e.g. IAM, you don't need to choose a Region for the AWS Management Console.

e.g.

- In the navigation bar, choose the name of the current Region.
- Choose a Region to switch to.

#### Setting default Region

See [Setting the default Region in the AWS Management Console](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/change-default-region.html)

### Search AWS services in AWS Management Console

### Add/Remove Favorite AWS services

### Create and use Dashboard Widgets

## 6. Creating Support Cases and Case Management in AWS

When need to contact AWS for technical and account support, you use **AWS Support**[^9] Center Console[^10]:

- **Account (and billing) support**
  - **Service quotas**[^11][^12]
- **Technical support**

> [!TIP]
> Create an alias for your AWS account so IAM users don't need to remember your AWS account ID.
>
> - Instead of login to `https://ABCXYZABCXYZ.signin.aws.amazon.com/console`
> - IAM users can use `https://ALIAS.signin.aws.amazon.com/console`
>
> How to create an alias? `IAM / Dashboard / AWS Account / Account Alias`

[^1]: https://000001.awsstudygroup.com/
[^2]:
    **An AWS account** is a container for all the AWS resources you can create as an AWS customer.

    - By default, each AWS account will have a _root user_.

      - The _root user_ has full access within your AWS account, and root user permissions cannot be limited.

    - When you first create your AWS account, you will be assessing it as the _root user_.

[^3]: Don't use root user for any task where it's not required.
[^4]: With MFA, you add an extra _factor_ to the authentication of your AWS account.
[^5]: An _IAM user_ is an entity (you created in AWS) that represent a person/application that interacts with AWS.
[^6]:
    An _IAM user **group**_ is a collection of IAM users. Use groups to specify permissions for a collection of users.

    - _User **group**_ make it easier to manage the permissions of multiple users.
    - Any user (in an user group) has the permissions of the user group.

[^7]: AWS Support has many Plans:

    - Basic: Free for all accounts.
    - Developer, Business, Enterprise: monthly pricing - you pay to receive Premium Support from AWS.

    See <https://aws.amazon.com/premiumsupport/plans/>

[^8]: IAM user group is aka group.
[^9]: https://aws.amazon.com/support/
[^10]: https://support.console.aws.amazon.com/support/home#/
[^11]: Service quota is aka service limit, see https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html
[^12]: Some services quotas can be increased automatically without opening a _support case_, by using Service Quota service.
