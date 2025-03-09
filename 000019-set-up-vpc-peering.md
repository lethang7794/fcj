# Set up VPC Peering

See the workshop at <https://000019.awsstudygroup.com/>

## 1. Introduction

> [!IMPORTANT]
> A VPC Peering connection is a network **connection between two VPCs** that allows you to route traffic between them (using IPv4 or IPv6 _private_ addresses).
>
> - Instances in either VPC can communicate with each other as if they were on the _same network_.

> [!TIP]
> Network ACL is a type of stateless firewall at the subnet-level.
>
> - NCAL can only be assigned to the subnet, but not to each Instance within the subnet.

> [!IMPORTANT]
> Cross-Peering DNS is a feature of VPC Peering that allows resources within one VPC to **resolve DNS of _another VPC_**.

## 2. Preparation

### 2.1 Initialize CloudFormation Template

### 2.2 Create Security Group

> [!NOTE]
> Duplicate inbound rule? TODO
>
> - Type: All ICMP - IPv4 | Source: Anywhere
> - Type: All ICMP - IPv4 | Source: Custom 10.10.0.0/16 (HG VPC’s CIDR)

### 2.3 Create EC2 instance

## 3. Update Network ACL

## 4. Create Peering Connection

## 5. Configuring Route tables

## 6. Enable Cross-Peer DNS

## 7. Clean up resources
