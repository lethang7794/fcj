# Optimizing EC2 Costs with Lambda

See the workshop at <https://000022.awsstudygroup.com/>

## 1. Introduction

## 2. Preparation

### 2.1 Create VPC

### 2.2 Create Security Group

### 2.3 Create EC2 instance

### 2.4 Incoming Web-hooks slack

## 3. Create Tag for Instance

## 4. Create Role for Lambda

## 5. Create Lambda Function

### 5.1 Function start instance

> [!TIP]
> Use an environment for the Webhook URL.

> [!NOTE]
> To invoke the lambda function at 8:00 AM (UTC) on Monday to Friday:
>
> - Choose `Schedule pattern`
> - And use the following cron expression: `0 8 ? * MON-FRI *` (see [Setting a rule schedule](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-scheduled-rule-pattern.html))
>
> (The next invocation is the next day, not the day that the EventBridge rule is created.)

> [!TIP]
> The timezone using by Amazon EventBridge is UTC+0.

> [!TIP]
> The EventBridge cron expression is different from crontab expression. The same schedule with crontab is [`0 8 * * 1-5`](https://crontab.guru/#0_8_*_*_1-5)

### 5.2 Function stop instance

> [!NOTE]
> To invoke the lambda function at 17:00 PM (UTC) on Monday to Friday:
>
> - Choose `Schedule pattern`
> - And use the following cron expression: `0 17 ? * MON-FRI *` (see [Setting a rule schedule](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-scheduled-rule-pattern.html))

## 6. Check Result

> [!WARNING]
> If you invoke the lambda function every working day on Monday to Friday, you need to wait a day to check the result.

> [!TIP]
> You can manually test the lambda function to see if it can start/stop the EC2 instance.

## 7. Clean up resources

> [!NOTE]
> Don't forget to cleanup:
>
> - IAM role.
> - EC2 instance (Terminated it)
> - Security group
> - VPC
