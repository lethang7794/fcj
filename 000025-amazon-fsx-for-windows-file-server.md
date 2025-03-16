# Amazon FSx for Windows File Server

See the workshop at <https://000025.awsstudygroup.com/>

## 1. Introduction

## 2. Preparation

### 2.1 Create Environment

> [!TIP]
> The CloudFormation stack needs from 30 to 40 minutes to be created, which is mostly from the creation of the Microsoft AD directory.

> [!CAUTION]
> The CloudFormation template for the workshop doesn't work anymore.
>
> - `nodejs12.x` runtime is deprecated[^1].
>
>   ```
>   The resource AmiInfoFunction is in a CREATE_FAILED state
>
>   This AWS::Lambda::Function resource is in a CREATE_FAILED state.
>
>   Resource handler returned message: "The runtime parameter of nodejs12.x is no longer supported for creating or updating AWS Lambda functions. We recommend you use a supported runtime while creating or updating functions. (Service: Lambda, Status Code: 400, Request ID: 863dc936-4b77-4acd-a487-94cae73cc57c)" (RequestToken: 29130333-d58a-d6df-1c97-a285a751ce6f, HandlerErrorCode: InvalidRequest)
>   ```
>
> - You need to
>   - download the original template `fxsw-tutorial.yaml` (<https://s3.amazonaws.com/amazon-fsx/tutorial/windows/templates/fsxw-tutorial.yaml>) and replace the deprecated runtime (`nodejs12.x`) to a supported runtimes[^2] (e.g. `nodejs22.x`)
>   - Or download the updated `fxsw-tutorial.yaml` (Open <https://github.com/lethang7794/amazon-fsx-tutorial/blob/master/windows-file-server/templates/fsxw-tutorial.yaml> - then click _Download raw file_)
> - Then open CloudFormation console, create a new stack, and upload your local template file `fxsw-tutorial.yaml`.

> [!TIP]
> The original CloudFormation template doesn't respect the InstanceType parameter.

### 2.2 Create an SSD Multi-AZ file system

### 2.3 Create an HDD Multi-AZ file system

## 3. Create new file shares

> [!TIP]
> When replacing `windows_remote_powershell_endpoint` with the _Windows Remote PowerShell Endpoint_, keep the double quotes.
>
> After replaced, it looks like this
>
> ```
> $WindowsRemotePowerShellEndpoint = "fs-012abcxyz6897abcc.example.com"
> ```

> [!TIP]
> If you use Linux, you can use [Connections](https://apps.gnome.org/Connections/) app to access the Windows `Instance0`.

## 4. Test Performance

### With DiskSpd

> [!WARNING]
> The link to `DiskSpd.zip` doesn't work anymore.
>
> - Use this link: <https://github.com/microsoft/diskspd/releases/download/v2.0.21a/DiskSpd.zip>
> - Or use this code with the updated link
>
>   ```powershell
>   $client = new-object System.Net.WebClient
>
>   $client.DownloadFile("https://github.com/microsoft/diskspd/releases/download/v2.0.21a/DiskSpd.zip","C:\Tools\DiskSpd-2.0.21a\DiskSpd-2.0.21a.zip")
>
>   Expand-Archive -LiteralPath C:\Tools\DiskSpd-2.0.21a\DiskSpd-2.0.21a.zip -DestinationPath C:\Tools\DiskSpd-2.0.21a
>   ```

### With fio

> [!NOTE]
> Option 1:
>
> - Use Internet Explorer to download fio from this link <https://github.com/axboe/fio/releases/download/fio-3.39/fio-3.39-x64.msi>
> - Then run `fio-3.39-x64.msi` to install `fio`.
> - Open a new PowerShell window so `fio` is available.
> - For all code to test performance with fio, replace `C:\Tools\fio-3.16-x64\fio` with `fio`.
>
>   ```PowerShell
>   $random = $(Get-Random)
>   fio --randrepeat=1 --direct=1 --name="Z:\${env:computername}-$random.dat" --numjobs=1 --bs=64K --iodepth=32 --size=1024M --readwrite=write --rwmixwrite=100 --thread --time_based --runtime=120
>   ```

> [!NOTE]
> Option 2: Download `fio-3.16-x64.zip` from <https://bsdio.com/fio/releases/private/fio-3.16-x64.zip>
>
> - Extract the zip file to `C:\Tools\fio-3.16-x64\`
> - (So you have `fio.exe` in `C:\Tools\fio-3.16-x64\`)
> - Then you can use the code in the workshop.

## 5. Monitor Performance

## 6. Enable data deduplication

## 7. Enable shadow copies

## 8. Manage user sessions and open files

## 9. Enable user storage quotas

## 10. Enable Continuous Access share

> [!TIP]
> When map network drive, the folder should look like this `\\fs-0123456789abcdef.example.com\d$`

> [!WARNING]
> I encounter an error while enable Continuous Access share
>
> ```powershell
> [fs-08ccb1fda6897abcc.example.com]: PS>New-FSxSmbShare -Name "SQL CA Share" -Path "D:\sql" -Description "SQL CA share" -ContinuouslyAvailable $True -FolderEnumerationMode AccessBased -EncryptData $true
> >>
>
> Windows PowerShell Credential Request: cmdlet New-FSxSmbShare at command pipeline position 1
> Warning: A script or application on the remote computer FS-08CCB1FDA6897ABCC.EXAMPLE.COM is requesting your
> credentials. Enter your credentials only if you trust the remote computer and the application or script that is
> requesting them.
>
> Supply values for the following parameters:
> Credential
> The request is not supported.
>     + CategoryInfo          : InvalidOperation: (MSFT_SMBShare:ROOT/Microsoft/Windows/SMB/MSFT_SMBShare) [New-SmbShare
>    ], CimException
>     + FullyQualifiedErrorId : Windows System Error 50,New-SmbShare
>     + PSComputerName        : amznfsxnqlabugg.example.com
> ```

## 11. Scale throughput capacity

## 12. Scale storage capacity

## 13. Delete environment

- Delete SNS topic `High_Throughput_fs-...`.
- Delete CloudWatch alarm `High_Throughput_Alarm_fs-...`.
- Delete Amazon FSx `MAZ` file systems.
- Delete CloudFormation stack.

## 14. Using the AWS CLI (reference)

[^1]: https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html#runtimes-deprecated
[^2]: https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html#runtimes-supported
