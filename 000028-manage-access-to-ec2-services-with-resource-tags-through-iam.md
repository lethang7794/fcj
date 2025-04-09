# Manage Access To EC2 Services With Resource Tags Through IAM

See the workshop at <https://000028.awsstudygroup.com/>

## 1. Introduction

## 2. Preparation

### 2.1 Create IAM user

## 3. Create IAM Policy

## 4. Create IAM Role

## 5. Check Policy

> [!TIP]
> When a principal makes a request to AWS, AWS gathers the request information into a request context. You can use the `Condition` element of a JSON policy to compare
>
> - _keys_ in the request context with
> - key values that you specify in your policy

> [!NOTE]
> For more information, see
>
> - _[Condition **Operators**](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html)_ in IAM policy .
>
>   - `StringEquals`[^1]
>   - `ForAllValues:StringEquals`[^2]
>
> - [_Global **condition keys**_](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html)
>
>   - `aws:RequestedRegion`[^3]
>   - `aws:ResourceTag/tag-key`[^4]

> [!WARNING]
> The condition `StringEqualsIfExists` cannot be found in the docs.

### 5.1 Switch Roles

### 5.2 Check IAM Policy

#### 5.2.1 Initiating access to EC2 console in AWS Region - Tokyo

#### 5.2.2 Initiating access to EC2 console in AWS Region - North Virginia

> [!TIP]
> The new `EC2 dashboard`'s `Resource` section also shows `Auto Scaling Groups`. There will be 2 resources showing `API error`:
>
> - `Auto Scaling Groups`
> - `Load balancers`

#### 5.2.3 Proceed to create EC2 instance when there are no and qualified Tags

#### 5.2.4 Edit Resource Tag on EC2 Instance

#### 5.2.5 Policy Check

## 6. Clean up resources

> [!TIP]
> To go back to the original IAM user, select the role name in the top right corner of the page, then click `Switch Back`.

> [!WARNING]
> Check again whether you have terminated the EC2 instance in `us-east-1`.

> [!TIP]
> To find the policy that you created, you can use the `Filter by Type` with the value of `Customer managed`

[^1]: https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html#Conditions_String
[^2]: https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html#conditions_string_multivalued
[^3]: https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-requestedregion
[^4]: https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-resourcetag
