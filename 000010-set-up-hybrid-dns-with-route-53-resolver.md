# Set up Hybrid DNS with Route 53 Resolver

## 1. Introduction

- **Route 53**: AWS's DNS service
- **Route 53 _Resolver_**: facilitate a hybrid DNS architecture
  - **_Outbound_ Endpoints**: send DNS query to on-premises (DNS system)
  - **_Inbound_ Endpoints**: receive DNS queries from on-premises (DNS system)
  - (Route 53) **Resolver _Rules_**:

## 2. Preparation

> [!NOTE]
> AWS QuickStart[^1] has been renamed to AWS Solutions Library[^2]

> [!NOTE]
> AWS CloudFormation: IaC from AWS

> [!NOTE]
> AWS Directory Service: AWS service to deploy Microsoft's Active Directory on AWS

### Generate Key Pair

> [!TIP]
> To create a key pair, you use the EC2 service.

### Initiating CloudFormation Template

### Security Group Configuration

> [!TIP]
> You can access the security group from VPC or EC2 service.

## 3. Connecting to RDGW

## 4. Microsoft AD Deployment

## 5. Setup DNS

### Create Route 53 Outbound Endpoint

### Create Route 53 Resolver Rules

### Create Route 53 Inbound Endpoints

### Test Result

> [!WARNING]
> The workshop doesn't test inbound endpoint.
>
> How to test inbound endpoint?

## 6. Clean up resources

[^1]: <https://github.com/aws-quickstart>
[^2]: <https://aws.amazon.com/solutions/>
