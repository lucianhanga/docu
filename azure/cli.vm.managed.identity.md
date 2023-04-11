# VM system-assigned managed identity access Resource Manager

## Create a VM with system-assigned managed identity

Enablle the system-assigned managed identity on a VM by going to the portal and clicking on the Settings->Identity. In the System assigned tab, click on the Enable button. This will create a system-assigned managed identity for the VM.

With command line this can be done by running the following command:
```powershell
# get the VM name
$vmName = az vm list --query "[?contains(name, 'az204vm')].name" --output tsv
echo $vmName
# enable the system-assigned managed identity
az vm identity assign --name $vmName --resource-group az204-vm-rg

# get the VM identity
$vmIdentity = az vm identity show --name $vmName --resource-group az204-vm-rg --query "principalId" --output tsv
echo $vmIdentity
```

## Grant access to the VM system-assigned managed identity to a resource group

```powershell
# get the resource group id
$rgId=$(az group show --name az204-vm-rg | jq -r '.id')
echo $rgId

# grant read access to the VM identity
az role assignment create --role Reader --assignee $vmIdentity --scope $rgId
```


## Get a token for the VM system-assigned managed identity

 Login to the vm and open a bash shell. Run the following command to get a token for the VM system-assigned managed identity:

```bash
# get the token inside the VM !!!
token=$(curl "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/" -H "Metadata: true" | jq -r'[access_token?]')
echo $token

# get the subscription id - linux only - e.g. Azxure Cloud Shell
subscription=$(az account show | jq -r '.id')
echo $subscription
# get the group name - linux only - e.g. Azxure Cloud Shell
group=$(az group list --query "[?contains(name, 'europe')].name" --output tsv)
echo $group

# access the resource from inside the VM !!!
curl "https://management.azure.com/subscriptions/c3407f72-80bd-4627-ae31-d07cfe8adcb7/resourceGroups/cloud-shell-storage-westeurope?api-version=2016-06-01" -H "ContentType: application/json" -H"Authorization: Bearer $token"
```

the result should be something like:

```json
{
  "id": "/subscriptions/c3407f72-80bd-4627-ae31-d07cfe8adcb7/resourceGroups/cloud-shell-storage-westeurope",
  "name": "cloud-shell-storage-westeurope",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

