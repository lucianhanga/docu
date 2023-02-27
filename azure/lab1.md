
Install azure cli

```powershell
 $ProgressPreference = 'SilentlyContinue'; Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi
```

Login to azure

```powershell
az login
```


```powershell
az webapp list --resource-group ManagedPlatform-GNHKMU0W4G
az webapp list --resource-group ManagedPlatform-GNHKMU0W4G --query "[?starts_with(name, 'imgapi')]"
az webapp list --resource-group ManagedPlatform-GNHKMU0W4G --query "[?starts_with(name, 'imgapi')].{Name:name}" --output tsv
cd F:\Allfiles\Labs\01\Starter\API\
az webapp deployment source config-zip --resource-group ManagedPlatform-GNHKMU0W4G --src api.zip --name <name-of-your-api-app>

```