# Azure Container Registry

## Create a container registry

### using the Azure CLI

```powershell
# login to Azure
az login

# create the group
az group create --name acr1 --location westeurope

# create the registry
az acr create --resource-group acr1 --name acr1lucian --sku Basic

# create a fake docker file
echo "FROM mcr.microsoft.com/hello-world" > Dockerfile

# build the image
az acr build `
      --registry acr1lucian `
      --image hello-world:v1 `
      --file Dockerfile `
      . `
# list the images
az acr repository list --name acr1lucian --output table

# list  the tags
az acr repository show-tags `
      --name acr1lucian `
      --repository hello-world `
      --output table `

# run the image
az acr run `
      --registry acr1lucian `
      --cmd "docker run acr1lucian.azurecr.io/hello-world:v1" `
      /dev/null

# list only the running containers
az acr task list-runs `
      --registry acr1lucian `
      --output table `
      --status Running
    
# stop the container
az acr task cancel-run `
      --registry acr1lucian `
      --run-id 1e
```


### using the Azure Portal

```powershell
# login to Azure using the Azure PowerShell
Connect-AzureAccount

# create the group using Azure PowerShell
New-AzureRmResourceGroup -Name acr2 -Location westeurope

```

## Deploy a container instance - ACI

```powershell
# login to Azure
az login

# create the group
az group create --name aci1 --location westeurope

# create a random value
$RANDOM = Get-Random -Minimum 1000 -Maximum 9999
# dns name
$DNS_NAME_LABEL="aci-example-$RANDOM"
echo $DNS_NAME_LABEL

# create the container
az container create `
      --resource-group aci1 `
      --name aci1lucian `
      --image mcr.microsoft.com/azuredocs/aci-helloworld `
      --dns-name-label $DNS_NAME_LABEL `
      --ports 80 `
      --ip-address public `
      --location westeurope `
      --verbose `

# check if the container is running
az container show `
      --resource-group aci1 `
      --name aci1lucian `
      --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" `
      --out table

## specify also the restart policy
az container create `
      --resource-group aci1 `
      --name aci1lucian `
      --image mcr.microsoft.com/azuredocs/aci-helloworld `
      --dns-name-label $DNS_NAME_LABEL `
      --ports 80 `
      --ip-address public `
      --location westeurope `
      --restart-policy OnFailure `
      --verbose `

# specify the environment variables
az container create `
      --resource-group aci1 `
      --name aci1lucian `
      --image mcr.microsoft.com/azuredocs/aci-helloworld `
      --dns-name-label $DNS_NAME_LABEL `
      --ports 80 `
      --ip-address public `
      --location westeurope `
      --restart-policy OnFailure `
      --environment-variables `
      "PORT=80" `
      "WEBSITES_ENABLE_APP_SERVICE_STORAGE=false" `
      --verbose `

# mount a volume
az container create `
      --resource-group aci1 `
      --name aci1lucian `
      --image mcr.microsoft.com/azuredocs/aci-helloworld `
      --dns-name-label $DNS_NAME_LABEL `
      --ports 80 `
      --ip-address public `
      --location westeurope `
      --azure-file-volume-account-name $STORAGE_ACCOUNT_NAME `
      --azure-file-volume-account-key $STORAGE_ACCOUNT_KEY `
      --azure-file-volume-share-name $STORAGE_ACCOUNT_SHARE_NAME `
      --azure-file-volume-mount-path /aci/logs `
      --verbose `      

```





