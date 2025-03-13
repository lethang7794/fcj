# VM Import/Export

## 1. VMWare Workstation

> [!TIP]
> If you use Linux, you can use Gnome Boxes.

## 2. Import virtual machine to AWS

### 2.1 Export virtual machine from On-premises

> [!WARNING]
> Not all the OS can be imported to AMI, see: [Operating systems supported by VM Import/Export](https://docs.aws.amazon.com/vm-import/latest/userguide/prerequisites.html#vmimport-operating-systems)

> [!TIP]
> Use `qemu-img convert` to convert
>
> - from the format of Gnome Boxes (`qcow2`)
> - to a format supported by `aws ec2 img-import`: OVA | VHD | VHDX | VMDK | RAW
>
> ```bash
> qemu-img convert -pO vhdx ubuntu12.04 ubuntu12.04.vhdx
> ```
>
> Ref:
>
> - <https://stackoverflow.com/questions/52724010/how-to-export-virtual-machine-from-fedora-gnome-boxes-to-virtual-box>
> - <https://docs.aws.amazon.com/cli/latest/reference/ec2/import-image.html#:~:text=The%20format%20of%20the%20disk%20image%20being%20imported>.

### 2.2 Upload virtual machine to AWS

### 2.3 Import virtual machine to AWS

### 2.4 Deploy Instance from AMI

## 3. Export instance from AWS

### 3.1 Setting up S3 bucket ACL

### 3.2 Export virtual machine from Instance

> [!TIP]
> On Linux
>
> - Input task as parameter
>
>   ```bash
>   aws ec2 create-instance-export-task --instance-id <INSTANCE_ID> --target-environment vmware --export-to-s3-task DiskImageFormat=vmdk,ContainerFormat=ova,S3Bucket=<SE_BUCKET_NAME>,S3Prefix=exported-vms
>   ```
>
> - Load parameter from file
>
>   ```bash
>   aws ec2 create-instance-export-task --instance-id <INSTANCE_ID> --target-environment vmware --export-to-s3-task file://export-spec.json
>   ```
>
>   See: <https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-parameters-file.html>

### 3.3 Export virtual machine from AMI

## 4. Reference video

## 5. Resources cleanup
