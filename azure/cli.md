# Azure - Command Line Interface (CLI)

### Install the Azure CLI on Ubuntu

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

or

[Install the Azure CLI on Ubuntu](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt)


### Install the Azure CLI on Windows

```powershell
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; Remove-Item .\AzureCLI.msi
```

or

[Install the Azure CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli)

Don't forget to restart the powershell after installation. And make sure you have the latest version of the Azure CLI.

```powershell
 az version
 az upgrade
```

Login to Azure

```powershell
az login
```

### Install the functions core tools

```powershell
npm install -g azure-functions-core-tools@3 --unsafe-perm true
```

or 

[Install the functions core tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=windows%2Ccsharp%2Cbash#v2)


### Create a Web App

[Azure Apps webpage](https://learn.microsoft.com/en-us/azure/app-service/overview)

```powershell
# create a new wen app in command line
dotnet new webapp -f net6.0
# run the application locally
dotnet run --urls=https://localhost:5001/
```

```powershell
# list all the applications available on  Azure
az webapp list --query "[].{hostName: defaultHostName, state: state}"
```

```powershell
# publish the application to Azure
az webapp up --sku F1 -n <app-name>
```
