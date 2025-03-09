# Cost Management with AWS Budgets

See the workshop at <https://000007.awsstudygroup.com/>

> [!TIP]
> In _root user_ of your AWS account, enable `IAM user/role access to Billing information` so you can use IAM user `AdminUser` to access billing information (including `AWS Budgets` service).
>
> See <https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started-account-iam.html#billing-access>

Overview:

- **AWS Budgets**: Set custom **budgets** that _alert_ you when you _exceed_[^1] your budgeted thresholds.

- _Budget types_:

  - **Cost** budget: Total cost of your AWS account
  - **Usage** budget: Cost of services
  - **Savings Plan** budget (utilization/coverage)
  - **RI** budget (utilization/coverage)

## 1. Create Budget by template

> [!WARNING]
> To access cost & usage data of a new accounts, you may need to wait up to 24 hours after you first:
>
> - visit the Billing and Cost Management console, [see more](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-enable.html)
> - create a budget in AWS Budgets (which under the hood use AWS billing data)

## 2. Creating a Cost Budget

> [!TIP]
> Cost budget is the only type of budget you can create immediately for a new account.

## 3. Creating a Usage Budget

- For my account, I need to wait 24 hour for cost & usage data before creating usage budget.

## 4. Creating an Reservation Budget

## 5. Creating a Savings Plans Budget

## 6. Resource Cleanup

## Notes

- Update frequency

  - AWS Budgets information is updated up to three times a day.
    - Updates typically occur 8–12 hours after the previous update
  - AWS billing data, which Budgets uses to monitor resources, is updated at least once per day.

- Advantage budget:

  You can customize a lot of aspects of the budget:

  - Budgeted thresholds

    - The period to be tracked: Daily - Monthly - Quarterly - Annually.
    - The renewal type: Fixed - Planned (for each period)
    - The budgeted amount

  - Budget scope

    - All services
    - Filter specific AWS cost dimensions:
      - Service, e.g. `EC2`, `RDS`
      - Region, e.g. `us-east-1`, `ap-southeast-1`
      - Tag, e.g. `dev`, `prod`
      - ...

  - When will you be alerted, e.g.
    - For the _monthly cost budget_ template, you will be notified when:
      - your **actual spend** reach `85%`
      - your actual spend reach `100%`
      - your **forecasted spend** reach `100%`
    - For the _zero spend budget_, you will be notified via email when any spend above `$0.01` is incurred.

## For more information

- [AWS Budgets documentation](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html)

[^1]: AWS Budgets can predict that you would exceed your budget, and alert you early.
