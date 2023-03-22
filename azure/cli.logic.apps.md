# Azure Logic Apps from CLI and Azure Powershell

## Create a Logic App from CLI

```powershell

# login to the azure
az login

# create the group
az group create `
      --name  lh-logicapps-flowcontrol `
      --location eastus `

# create a storage container for the logic app
az storage account create `
      --name lhlogicappsflowcontrol `
      --resource-group lh-logicapps-flowcontrol `
      --location eastus `
      --sku Standard_LRS  `

# list the storage accounts
az storage account list `
      --resource-group lh-logicapps-flowcontrol `
      --query "[].{name:name, key:primaryEndpoints.table}" `
      --output table

# get the first connection string
az storage account show-connection-string `
      --name lhlogicappsflowcontrol `
      --resource-group lh-logicapps-flowcontrol `
      --query connectionString `
      --output tsv

# get the keys of the storage account
az storage account keys list `
      --account-name lhlogicappsflowcontrol `
      --resource-group lh-logicapps-flowcontrol `
      --query "[].{name:keyName value:value }" `
      --output tsv

# create a container 
az storage container create `
      --name demo `
      --account-name lhlogicappsflowcontrol `
      --account-key  KFoxssZMbD3l+nh53tvOp/nXj/cjZV3NJSDTLo7TBxfzUlvJti/cDLoJH8Zgki9MuPsYQ+e0aivv+AStG2Lh0g== `
      --public-access off

# create a table
az storage table create `
      --name demo `
      --account-name lhlogicappsflowcontrol `
      --account-key  KFoxssZMbD3l+nh53tvOp/nXj/cjZV3NJSDTLo7TBxfzUlvJti/cDLoJH8Zgki9MuPsYQ+e0aivv+AStG2Lh0g== `

```      
