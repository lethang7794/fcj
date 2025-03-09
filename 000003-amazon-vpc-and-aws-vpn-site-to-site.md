# Amazon VPC and AWS VPN Site-to-Site

See the workshop at <https://000003.awsstudygroup.com/>

> [!TIP]
> VPC vs VPN
>
> - VPC: Virtual Private Cloud
> - VPN: Virtual Private Network

## 1. Introduction to VPC

|                            | What is it?                                                                                                                                | What you can do?                                                                                                                                                                                                                                   |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **VPC**                    | A logically isolated section of the AWS Cloud virtual **network** that you defined                                                         | You have _full control_ your virtual networking environment - including resource placement, connectivity, and security - by:<br/>- selecting your own IP address range<br/>- creating subnets<br/>- configuring route tables and network gateways. |
| **Subnet**                 | A _segment_ of the **IP address range** of a Amazon VPC that AWS resources (e.g. an EC2 instance) can be attached to.                      | You can create subnets to _group resources_ according to security and operational needs.                                                                                                                                                           |
| **Route Table**            | A set of **routing rules** that controls the _traffic leaving_ any subnet that's associated with the route table.                          | You can associate multiple subnets with a single route table, but a subnet can be associated with only one route table at a time.                                                                                                                  |
| **Internet Gateway** (IGW) | A resource that _connects a **network** to the internet_.                                                                                  | You can route traffic for IP addresses _outside_ your Amazon VPC to the internet gateway.                                                                                                                                                          |
| **NAT Gateway** (NATGW)    | A **NAT device**, managed by AWS, that performs _network address translation_ in a _private subnet_, to secure _inbound_ internet traffic. | You can use a NAT gateway (in a public subnet with an elastic IP address) so that:<br/>- instances in a private subnet can connect to services outside your VPC<br/>- but external services cannot initiate a connection with those instances      |

|                      | Default                                                                       | Custom |
| -------------------- | ----------------------------------------------------------------------------- | ------ |
| **VPC**              | `172.31.0.0/16`                                                               |        |
| **Subnet**           | `/20`                                                                         |        |
| **Route Table**      | Destination - Target<br/>`172.31.0.0/16` - `local`<br/>`0.0.0.0/0` - `IGW-id` |        |
| **Internet Gateway** |                                                                               |        |
| **NAT Gateway**      |                                                                               |        |

### VPC

#### Default VPC

A default VPC comes with a public subnet in each Availability Zone, an internet gateway, and settings to enable DNS resolution

|                  | Default VPC components                                                                           |                                                                               |
| ---------------- | ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------- |
| VPC              | `/16` IPv4 CIDR block (`172.31.0.0/16`)                                                          |                                                                               |
| Subnet           | `/20` default subnet in each Availability Zone                                                   |                                                                               |
| Route Table      | A _main route table_ with a route that points all traffic (`0.0.0.0/0`) to the internet gateway. | Destination - Target<br/>`172.31.0.0/16` - `local`<br/>`0.0.0.0/0` - `IGW-id` |
| Internet Gateway | Connected to your default VPC.                                                                   |                                                                               |
| Security Group   | A default security group that is associated with your default VPC                                |                                                                               |
| NACL             | A default NACL is associated with your default VPC                                               |                                                                               |
| DHCP options     | The default DHCP options set for your AWS account is associated with your default VPC            |                                                                               |

### Subnets

### Route Table

### Internet Gateway

### NAT Gateway

## 2. Firewall within VPC

|                    | Non-default                                                                                                                                           | Default                                                                                                                                                                      |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Security Group** | **Inbound rules**: <br/>No inbound rules when first created                                                                                           | **Inbound rules**: <br/>Source - Protocol - Ports <br/>`sg-id` - `All` - `All`                                                                                               |
|                    | **Outbound rules**:<br/>Destination - Protocol - Ports<br/>`0.0.0.0/0` - `All` - `All`                                                                | **Outbound rules**:<br/>Destination - Protocol - Ports<br/>`0.0.0.0/0` - `All` - `All`                                                                                       |
| **NACL**           | **Inbound rules**:<br/>Rule # - Source - Protocol - Ports - Allow/Deny<br/>`*` - `0.0.0.0/0` - `All` - `All` - `Deny` (_Default inbound rule_)        | **Inbound rules**:<br/>Rule # - Source - Protocol - Ports - Allow/Deny<br/>`100` - `0.0.0.0/0` - `All` - `All` - `Allow`<br/>`*` - `0.0.0.0/0` - `All` - `All` - `Deny`      |
|                    | **Outbound rules**:<br/>Rule # - Destination - Protocol - Ports - Allow/Deny<br/>`*` - `0.0.0.0/0` - `All` - `All` - `Deny` (_Default outbound rule_) | **Inbound rules**:<br/>Rule # - Destination - Protocol - Ports - Allow/Deny<br/>`100` - `0.0.0.0/0` - `All` - `All` - `Allow`<br/>`*` - `0.0.0.0/0` - `All` - `All` - `Deny` |

## 3. Preparation Steps

### Create VPC

> [!TIP]
> After you created a VPC, AWS Management Console will show you the detail of your created VPC.

### Create Subnet

> [!TIP]
> After you created a subnet, AWS Management Console will show you the filtered subnet list with your created subnet.
>
> - Select your subnet to see its detail.

> [!TIP]
> This is a bug in AWS Management Console, if you try to refresh the link after you created a subnet, that subnet will be selected, and you will see the detail of it.

### Create Internet Gateway

### Create Route Table

- Create a new route table for public subnets

### Create Security Group

> [!NOTE]
> There is already a default security group for your created VPC.
>
> This security group allows:
>
> - Inbound traffic from other instances that has the same security group
> - All outbound traffic
>
> which is too broad in security perspective (and not enough for our needs).

We will create 2 new security groups:

- A security group for instances in the public subnets:
  - Allow SSH and ping from anywhere (inbound rules)
  - Allow all traffic to anywhere (outbound rules) - the _default outbound rule_.
- Another security group for instances the the private subnets:
  - Allow SSH and ping from instances in public subnets (to instances private subnets) (inbound rules)
  - Allow all traffic to anywhere (outbound rules) - the _default outbound rule_.

> [!CAUTION]
> You can't change the description of a security group using the AWS Management Console.

## 4. Creating an EC2 Server

> [!TIP]
> Amazon Linux 2023 is the successor to Amazon Linux 2.

> [!TIP]
> There is also a smaller, cheaper instance `t2.nano`[^1] - but `t2.nano` is not eligible with free tier.

### Create EC2 Server

### Test Connection

> [!NOTE]
> The address in example to connect to the EC2 instance is using DNS name instead of IP address.

> [!TIP]
> Although you use public IP address to SSH to the public instance, the terminal prompt will show the private address of the instance.

### Create NAT Gateway

> [!TIP]
> Disconnect from private instance then re-connect.

### Using Reachability Analyzer

> [!TIP]
> Reachability Analyzer is in Network Manager service.

## 5. Configuration of Site-to-Site VPN

### 5.1 Create a VPN environment

- You use a AWS Site-to-Site VPN connection to connect your remote network to a VPC.

- When creating a AWS Site-to-Site VPN connection:

  - First, you need a VPG and CGW:

    - VPG: the component in AWS-site
    - CGW: the component in client-site

  - Then you specify a VPN Tunnel routing type:

    - Static routing:

      - You manually specify routes between VPG and CGW.
      - VPC needs to be enabled routes propagations.

    - Dynamic routing: If CGW support BGP, you can use dynamic route and let devices uses BGP advertise its routes

    > [!TIP]
    > VPN tunnel connections are initiated from CGW to VPG.

  - .... update the route table for your subnet (to route traffic to VGW)

> [!NOTE]
> When to static routing and dynamic routing?
>
> - Prefer dynamic routing when possible
> - Use static routing when there are identical routes exist in the virtual private gateway

#### 5.1.1 Create VPC for VPN

#### 5.1.2 Create EC2 as a Customer Gateway

### 5.2 Configure VPN Connection

#### 5.2.1 Create Virtual Private Gateway

#### 5.2.2 Create Customer Gateway

#### 5.2.3 Create VPN Connection

#### 5.2.4 Customer Gateway Configuration

#### 5.2.5 Modify AWS VPN Tunnel

### 5.3 VPN Connection using Strongswan with Transit Gateway (Optional)

#### 5.3.1 Create Virtual Private Gateway

#### 5.3.2 Create Customer Gateway

#### 5.3.3 Create VPN Connection

#### 5.3.4 Create Transit Gateway Attachment

#### 5.3.5 Configure Route Tables

#### 5.3.6 Configuring Customer Gateway

## 6. Resource Cleanup

- Delete EC2 instance
- Delete NAT Gateway
- Delete (release) Elastic IP address

> [!TIP]
> We need to wait still the Elastic IP address can be associated again.

- Delete VPC:

> [!TIP]
> Delete a VPC will also delete its: subnets, route tables, internet gateway, security groups, NACLs.

- Delete Reachability Analyzer path

[^1]: <https://aws.amazon.com/about-aws/whats-new/2015/12/introducing-t2-nano-the-smallest-lowest-cost-amazon-ec2-instance/>
