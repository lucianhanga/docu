# Azure Storage Message Queue

## Create a queue

### using the Azure CLI

```powershell
# login to Azure
az login

# create the group
az group create --name stq1 --location westeurope

# create the storage account
az storage account create `
      --resource-group stq1 `
      --name stq1lucian `
      --location westeurope `
      --sku Standard_LRS `

# create the queue
az storage queue create `
      --account-name stq1lucian `
      --name stq1lucian `
      --output table `
```

