# Set up AWS Transit Gateway

See the workshop at <https://000020.awsstudygroup.com/>

## 1. Introduction

> [!IMPORTANT]
> Why Transit Gateway?
>
> - Connect VPCs in a central hub style, which is simpler than VPC Peering.

> [!TIP]
> Transit Gateway can also connect VPC to on-premises networks.

> [!NOTE]
> How to connect a VPC to a Transit Gateway?
>
> ---
>
> To connect a VPC to a Transit Gateway, you:
>
> - **attach a subnet** from _each AZ_ (of that VPC) via the _Transit Gateway Attachment_ to the Transit Gateway
> - (route traffic to the transit gateway - using TWG route table)
>
>   - create a TGW route table
>     - create associations to associate the TGW route table with the TGW attachments
>     - create propagations to allow routes to be propagated from an attachment to the target TGW route table.
>   - route traffic from each VPC to the TGW route table

## 2. Preparation

### 2.1 Generate Key Pair

### 2.2 Initialize CloudFormation Template

## 3. Create Transit Gateway

## 4. Create Transit Gateway Attachments

## 5. Create Transit Gateway Route Tables

## 6. Add Transit Gateway Routes to VPC Route Tables

## 7. Clean up resources

> [!TIP]
> You need to delete the TGW attachments before delete a TGW.
>
> - TGW route table will be deleted automatically when the TGW is deleted.
