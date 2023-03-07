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

### List IP addresses

```bash
IPADDRESS="$(az vm list-ip-addresses \
  --resource-group learn-68a1776c-a86a-4243-991c-fd71246767b7 \
  --name my-vm \
  --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
  --output tsv)"
# show the ipaddress
echo $IPADDRESS
# test if the webpage works
curl --connect-timeout 5 http://$IPADDRESS
```

### List the Network Security Group

Every VM on Azure is associated with at least one network security group. In this case, Azure created an NSG for you called `my-vmNSG`.

```bash
az network nsg list \
  --resource-group learn-68a1776c-a86a-4243-991c-fd71246767b7 \
  --query '[].name' \
  --output tsv
```

list command to list the rules associated with the NSG named `my-vmNSG`:

```bash
az network nsg rule list \
  --resource-group learn-68a1776c-a86a-4243-991c-fd71246767b7 \
  --nsg-name my-vmNSG
# or the short version of the output
az network nsg rule list \
  --resource-group learn-68a1776c-a86a-4243-991c-fd71246767b7 \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table
```
The last command listed above, use the --query argument to retrieve only the name, priority, affected ports, and access (Allow or Deny) for each rule.
The priority of this rule is 1000. Rules are processed in priority order, with lower numbers processed before higher numbers.

### Create a new rule in NSG

create a rule called `allow-http` that **allows inbound access on port 80**:

```bash
az network nsg rule create \
  --resource-group learn-68a1776c-a86a-4243-991c-fd71246767b7 \
  --nsg-name my-vmNSG \
  --name allow-http \
  --protocol tcp \
  --priority 100 \
  --destination-port-range 80 \
  --access Allow
```