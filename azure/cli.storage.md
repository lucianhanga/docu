# CLI and PowerShell commands for Azure Storage

## Manage a storage account using CLI

```powershell
# login to the azure
az login

# create the group
az group create --name lucianstoragegroup --location westus

# create the storage account
az storage account create `
    --name lucianstorageaccount2022 `
    --resource-group lucianstoragegroup `
    --location westus `
    --sku Standard_LRS `

# list the storage accounts
az storage account list `
  --query "[?starts_with(name, 'lucianstorageaccount')].{name:name, location:location, resourceGroup:resourceGroup}" `
  --output table `

# create a container in the storage account
az storage container create `
  --name luciancontainer1 `
  --account-name lucianstorageaccount2022 `
  --public-access off ` # blob, container, off

# upload a file to the container
az storage blob upload `
  --container-name luciancontainer1 `
  --account-name lucianstorageaccount2022 `
  --file "C:\Users\lucia\index.html" `
  --name test.txt `

# list all the blobs from the container
az storage blob list `
  --container-name luciancontainer1 `
  --account-name lucianstorageaccount2022 `
  --query "[].{name:name, size:properties.contentLength}" `
  --output table `

# delete a blob from the container
az storage blob delete `
  --container-name luciancontainer1 `
  --account-name lucianstorageaccount2022 `
  --name test.txt `

# change the public access of the container
az storage container set-permission `
  --name luciancontainer1 `
  --account-name lucianstorageaccount2022 `
  --public-access blob `

# copy a file between two containers
az storage blob copy start `
  --destination-blob test.txt `
  --destination-container luciancontainer2 `
  --source-account-name lucianstorageaccount2022 `
  --source-account-key <key> `
  --source-container luciancontainer1 `
  --source-blob test.txt `
```

## Policy for a storage account using CLI

```powershell

# list the policies
az storage account management-policy show `
  --account-name lucianstorageaccount2022 `
  --resource-group lucianstoragegroup `
  --output table `

# download the policy and save it to a file
az storage account management-policy show `
  --account-name lucianstorageaccount2022 `
  --resource-group lucianstoragegroup `
  --output jsonc `
  > policy.json


# create a policy
az storage account management-policy create `
  --account-name lucianstorageaccount2022 `
  --resource-group lucianstoragegroup `
  --policy ./policy.json `
  --output table `

# update a policy
az storage account management-policy update `
  --account-name lucianstorageaccount2022 `
  --resource-group lucianstoragegroup `
  --set policy.rules[0].definition.filters.prefixMatch[0]=test `
  --output table `

# delete the policy
az storage account management-policy delete `
  --account-name lucianstorageaccount2022 `
  --resource-group lucianstoragegroup `
  --output table `

```
