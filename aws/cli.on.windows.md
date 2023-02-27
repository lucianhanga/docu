#AWS CLI on Windows

Install the AWS CLI on Windows using the MSI installer.

```powershell
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi /qn
```

Syncronizing a S3 bucket to a local folder

```powershell
aws s3 sync myfolder s3://mybucket/myfolder
```

