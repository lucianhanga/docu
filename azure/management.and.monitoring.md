# Azure Management and Monitoring

## Azure Management Portal 

- **Azure Management Portal** is a web-based **management console** that enables you to manage all** **Azure services** from one place.

- **Dashboard** is the default view of the Azure Management Portal. It provides a single view of all the resources in your Azure account.

## Azure PowerShell

**Azure PowerShell** is a set of PowerShell **cmdlets** that enable you to manage **Azure** resources from the **Windows PowerShell** command line.
  
```powershell
# install the Azure PowerShell module
# -Name: the name of the module to install - in this case, the Azure PowerShell module
# -AllowClobber: allows the installation of the module even if it overwrites existing commands
# -Scope: the scope of the module installation - in this case, the current user
Install-Module -Name Az -AllowClobber -Scope CurrentUser
Import-Module -Name azuread # import the Azure Active Directory module
```

to get help on a cmdlet:

```powershell
Get-Help -Name Get-AzResourceGroup -Full
# or 
help Get-AzResourceGroup -ShowWindow
```


## Azure CLI

**Azure CLI** is a **command-line** **interface** that enables you to manage **Azure** resources from the **command line**.

## Azure Cloud Shell

**Azure Cloud Shell** is a browser-based **CLI** that enables you to manage Azure from the browser.


## Azure Mobile App

- track the status of your Azure resources
- diagnose and resolve issues
- run scripts and commands in CLI

## Azure REST API

- for developers to access Azure services programmatically


## Monitoring and Analytics Overview

### Azure Advisor

- **Azure Advisor** is a **personalized** **recommendation** engine that helps you follow best practices to optimize your Azure deployments.
  - reliability
  - security
  - Performance
  - Cost
  - Operational Excellence

### Azure Monitor

- **Activity Log** - records all the operations that are performed on resources in your Azure subscription.
- **Metrics** - collects and aggregates data from a variety of sources to provide insights into the health and performance of your resources.


### Service Health

- Provides information about the health of Azure services.




