# Resource Group CLI & PowerShell Commands

## Get information about the subscription and tenant

```powershell
az login
Connect-AzAccount
# List all the subscriptions
az account list
# List all the subscriptions using powershell
Get-AzSubscription
# getting help on powershell commands
Get-Help Get-AzSubscription -Online

az account list --query "[].{tenantId: tenantId, name: name}" --output tsv
# get the current subscription name in a variable
$name =$(az account list --query "[].{name: name}" --output tsv)
# get the current subscription id in a variable
$id =$(az account list --query "[].{id: id}" --output tsv)
# get the current subscription tenant id in a variable
$tenantId =$(az account list --query "[].{tenantId: tenantId}" --output tsv)
echo $name $id $tenantId
```

## Resource Group CLI Commands

### list and create resource groups

```powershell
# List all the locations
az account list-locations

# List all the resource groups
az group list 
# List all the resource groups using powershell
Get-AzResourceGroup

# Create a resource group
az group create --name resource1 --location westeurope
# Create a resource group using powershell
New-AzResourceGroup -Name resource1 -Location westeurope

# Create a resource group in a subscription
az group create `
    --name lucian_group66 `
    --location westeurope `
    --subscription $id `
    --tags "owner=Lucian" "environment=dev" `
# list all the resource groups, format output for names only
az group list --query "[].{name: name}" --output tsv
# list all the resource groups from a location
az group list --query "[?location=='westeurope'].{name: name}" --output tsv

# list all the resource groups with a tag
az group list --query "[?tags.owner=='Lucian'].{name: name}" --output tsv

# list all the resource groups with a tag using powershell and convert to json
Get-AzResourceGroup -Tag @{owner="Lucian"} | ConvertTo-Json
```

### delete resource groups

```powershell
# delete a resource group
az group delete --name resource1
# delete a resource group using powershell
Remove-AzResourceGroup -Name resource1
```

### add/remove locks to a resource group

```powershell
# add/remove a lock to a resource group
az lock create `
  --name lock1 `
  --resource-group resource1 `
  --lock-type CanNotDelete `
  --notes "This is a lock" `

# list all the locks
az lock list --resource-group lucian_group66

# add a lock to a resource group using powershell
New-AzResourceLock `
    -Name lock2 `
    -ResourceGroupName resource1 `
    -LockLevel CanNotDelete `
    -Notes "This is a lock" `

# list all the locks using powershell
Get-AzResourceLock `
    -ResourceGroupName resource1 `

# remove a lock from a resource group
az lock delete `
    --name lock1 `
    --resource-group resource1 `

# remove a lock from a resource group using powershell
Remove-AzResourceLock `
    -Name lock2 `
    -ResourceGroupName resource1 `
```

### list all the resources in a resource group

```powershell
# list all the resources in a resource group
az resource list --resource-group lucian_group66
# list all the resources in a resource group using powershell
Get-AzResource -ResourceGroupName lucian_group66
```
