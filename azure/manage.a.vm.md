# VM in Azure

## Create a VM using the az CLI

### Find all exisiting locations

```bash
# list all available locations
az account list-locations --output table
# or
az account list-locations -o tsv | cut -f 4 -d $'\t'
```

### List all existing groups

```bash
# list all resource groups
az group list --output table
# or 
az group list --output tsv  | cut -f4,2 -d $'\t' 
```

```bash
# first create a resource group
az group create --name test-vm-from-azure-shell --location westeurope
```
output:

```json
{
  "id": "/subscriptions/c3407f72-80bd-4627-ae31-d07cfe8adcb7/resourceGroups/test-vm-from-azure-shell",
  "location": "westeurope",
  "managedBy": null,
  "name": "test-vm-from-azure-shell",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```

if the group already exists and you try to create it again you don't get an error but the group is not created again.

### Create the vm

list all the existing machines

```bash
az vm list --output table
```

list all the available images in a location

```bash
az vm image list --location westeurope --output table
```

list all the prices for a specific image by location and publisher

```bash
az vm image list-offers --location westeurope --publisher Canonical --output table
```

Creating the vm

```bash
az vm create \
    --resource-group test-vm-from-azure-shell \
    --name vm_lucian_1 \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

if successful the following output will appear:

```json
{
  "fqdns": "",
  "id": "/subscriptions/c3407f72-80bd-4627-ae31-d07cfe8adcb7/resourceGroups/test-vm-from-azure-shell/providers/Microsoft.Compute/virtualMachines/vm_lucian_1",
  "location": "westeurope",
  "macAddress": "00-0D-3A-44-5E-43",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.57.232",
  "resourceGroup": "test-vm-from-azure-shell",
  "zones": ""
}
```
install nginx from github, azure examples

```bash 
az vm extension set \
  --resource-group test-vm-from-azure-shell \
  --vm-name vm_lucian_1 \
  --name customScript \
  --publisher Microsoft.Azure.Extensions \
  --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' \
  --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```

