## Azure PowerShell 

### Install the Azure PowerShell module

first make sure that you have the latest version of PowerShell

```powershell
# check the version
```

install version 7.x

```powershell
# install the latest version of PowerShell
winget search Microsoft.PowerShell
winget install --id Microsoft.Powershell --source winget
```
install the Azure PowerShell module

```powershell
Install-Module -Name Az -AllowClobber -Scope CurrentUser
# or 
Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force

# login to Azure
Connect-AzAccount
```



##  Azure - Command Line Interface (CLI)

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

## GitHub CLI

Windows PowerShell installation.
First install `scoop`:


```powershell
# Optional: Needed to run a remote script the first time
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser 

irm get.scoop.sh | iex
```

install the github cli

```powershell
scoop install gh
```

clone a repo:
```powershell
gh auth login
gh repo clone lucianhanga/azure.devel
```

## JMSEPath - Query Azure CLI

[JMSEPath refence](http://jmespath.org)


`[?Title == 'Demo 1']`

`[?contains(Title, 'Demo')]`

`[?contains(*, 'Demo 1')]` - would return **any** item in the array where the value of **any** property would be **Demo 1**

`[?starts_with(Title, 'Demo')]`

`[?contains(Title, 'Demo') || contains(Title, 'Demo 2')]` - would return **any** item in the array where the value of **any** property would be **Demo 1** or **Demo 2**

`[?contains(Title, 'Demo 1) && contains(Title, 'Demo 2')]` - would return **any** item in the array where the value of **any** property would be **Demo 1** and **Demo 2**

`[?contains(Title, 'Demo 1') && contains(Title, 'Demo 2')].{Title: Title, Id: Id}` - would return **any** item in the array where the value of **any** property would be **Demo 1** and **Demo 2** and return only the **Title** and **Id** properties

`[*].{Title: Title}` returns **all** items as array with a Title property.

if the filter is applied on an object rather then a list of objects, and `value` is a property of the object, then the filter would be applied on the `value` of the property.
`value[?Title == 'Garth North']`

`value[?contains(Email, 'contoso')]`

### Sorting

`sort_by(@, &"Last Activity Date")`

`reverse(sort_by(@, &"Last Activity Date"))`

`reverse(sort_by(@, &"Viewed Or Edited File Count")) | [0]."User Principal Name"` -  would sort and return the User Principal Name for the user with the most edited files.

`reverse(sort_by(@, &"Viewed Or Edited File Count")) | [?"Is Deleted" == 'False']."User Principal Name"` sorts by then Viewed Or Edited File Count, then filters out deleted users and finally returns the User Principal Name

`reverse(sort_by(@, &"Viewed Or Edited File Count")) | [0:3]."User Principal Name"` - to get the top 3 items


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
# install dev certificates
dotnet dev-certs https --trust
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
