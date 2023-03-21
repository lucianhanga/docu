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

Reference:

[Create ARM templates with Visual Studio Code](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-visual-studio-code?tabs=CLI)

Deploy the virtual machine using the Azure CLI:

```powershell
# Create a resource group for the VM
az group create --name vm-group2 --location westeurope
# deploy the VM
az deployment group create `
    --resource-group vm-group2 `
    --template-file template.json `
    --parameters parameters.json `
    --parameters adminPassword=MyPassword123 `
    --verbose `
# deploy the vm using powershell
New-AzResourceGroup -ResourceGroupName vm-group2 -Location eastus
$securePassword=ConvertTo-SecureString "MyPassword123" -AsPlainText -Force
New-AzResourceGroupDeployment `
    -ResourceGroupName vm-group2 `
    -TemplateFile template.json `
    -TemplateParameterFile parameters.json `
    -adminPassword $securePassword `
    -verbose `
    -AsJob `

# see the jobs
Get-Job
```

get the files from github: [template.json](https://github.com/lucianhanga/azure.devel/blob/main/vm.template.deployment/vm1.template/template.json) and [parameters.json](https://github.com/lucianhanga/azure.devel/blob/main/vm.template.deployment/vm1.template/parameters.json)

## Open a port on the VM

```powershell
# open a port on the VM
az vm open-port `
    --resource-group vm-group2 `
    --name vm1 `
    --port 80 `
    --priority 1000 `
    --verbose `
# open a port on a VM using azure powershell
# to be determined :)
```

## Specify the demployment mode

```powershell
# specify the deployment mode using CLI

az deployment group create `
  --mode Complete `
  --name ExampleDeployment `
  --resource-group ExampleResourceGroup `
  --template-file storage.json `

# specify the deployment mode using azure powershell
New-AzResourceGroupDeployment `
  -Mode Complete `
  -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
```
