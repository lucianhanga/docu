# Azure API with CLI

```powershell

# login to azure
az login

# create a group
az group create `
    --name az204-apim-rg `
    --location westeurope

# generate a random name for the api
$apiName = "az204-apim-" + (Get-Random -Minimum 1000 -Maximum 9999)
echo $apiName

# create the api
az apim create -n $apiName `
    --location westeurope `
    --publisher-email "tom@gmx.net" `
    --resource-group az204-apim-rg `
    --publisher-name AZ204-APIM-Exercise `
    --sku-name Consumption 

```

