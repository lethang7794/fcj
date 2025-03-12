# Using File Storage Gateway

See the workshop at <https://000024.awsstudygroup.com>

## 1. Preparation

### 1.1. Create S3 Bucket

### 1.2. Create EC2 for Storage Gateway

> [!TIP]
> The storage gateway will be hosted on EC2.

> [!TIP]
> Amazon S3 File Gateway requires TCP port `80` to be open for inbound traffic and one-time HTTP access during gateway activation. After activation, you can close this port.
>
> - If you plan to create NFS file shares, you must open
>   - TCP/UDP port `2049` for NFS access,
>   - TCP/UDP port `111` for NFSv3 access, and
>   - TCP/UDP port `20048` for NFSv3 access.
> - If you plan to create SMB file shares, you must open TCP port `445` for SMB access.

> [!WARNING]
> When creating security group, be careful with the protocol TCP or UDP of each rule.

### 2.1.Create Storage Gateway

### 2.2. Create File Shares

### 2.3. Mount File shares on On-premises machine

> [!TIP]
> The user to SSH into the EC2 instance is `admin` (not `root`)

> [!IMPORTANT]
> To mount NFS file share on Linux, use the IP of the EC2 instance (that host the File Gateway - aka _Host Platform_) instead of the File Gateway (the one showing in Example Commands).
>
> - The example command in the management console: `sudo mount -t nfs -o nolock,hard [GatewayIPAddress]:/[FileShareName] [MountPath]`
> - The correct command in the docs:`sudo mount -t nfs -o nolock,hard [GatewayVMIPAddress]:/[FileShareName] [ClientMountPath]`[^1]

## 3. Clean up resources

> [!TIP]
> On Linux, unmount the file share with `umount [ClientMountPath]`

[^1]: <https://docs.aws.amazon.com/filegateway/latest/files3/GettingStartedAccessFileShare.html>
