# Virtual Machines (VM) using CLI and PowerShell

## Create a VM

```powershell

# Create a resource group for the VM
az group create --name vm1 --location westeurope

# Create a simple VM
az vm create `
    --resource-group vm1 `
    --name vm1 `
    --image UbuntuLTS `
    --admin-username azureuser `
    --generate-ssh-keys `

# List the VM parameters
az vm list `
    --query "[?name == 'vm1'].{ name: name, vmSize: hardwareProfile.vmSize location: location}" `
    --output table `

# List all the VMs sizes available in a location
az vm list-sizes --location westeurope --output table

# filter for cheaper VMs
az vm list-sizes `
    --location westeurope `
    --query '[?numberOfCores <= `1` && memoryInMb <= `1024`]'


# change the VM size
az vm resize `
    --resource-group vm1 `
    --name vm1 `
    --size Standard_B1ls `

# shutdown the VM
az vm deallocate `
    --resource-group vm1 `
    --name vm1 `

# start the VM
az vm start `
    --resource-group vm1 `
    --name vm1 `

# delete the VM and all the resources
az group delete --name vm1

```

## Create a VM from a ARM Template

Creating an Azure virtual machine usually includes two steps:

- Create a **resource group**. An Azure resource group is a logical container into which Azure resources are deployed and managed. A resource group must be created before a virtual machine.
- Create a **virtual machine**.

