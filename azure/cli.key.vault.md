# Key Valut Management with Azure CLI

## Create a Key Vault

```powershell
# login to the azure
az login

# create the group
az group create --name luciankeyvaultgroup --location westus

# create the key vault
az keyvault create `
  --name luciankeyvault2023 `
  --resource-group luciankeyvaultgroup `
  --location westus `
  --sku standard `

# add a secret to the key vault
az keyvault secret set `
  --vault-name luciankeyvault2023 `
  --name luciansecret `
  --value "my secret"

# retrieve the secret from the key vault
az keyvault secret show `
  --vault-name luciankeyvault2023 `
  --name luciansecret `
  --query value `
  --output tsv

# delete the secret from the key vault
az keyvault secret delete `
  --vault-name luciankeyvault2023 `
  --name luciansecret

```

## Create a key vault and enable it for template deployment

```powershell

# install openssl for windows using scoop
scoop install openssl

# login to the azure
az login

# define all the variables
$RESOURCE_GROUP = "test-keyvault-rg"
$KEY_VAULT_NAME = "testkeyvaultlh2022"
$LOCATION = "westus"
$SUBSCRIPTION_ID = "9b79def9-4b73-4eac-886d-8ce529aacacd"


# create the group
az group create `
    --name $RESOURCE_GROUP `
    --location $LOCATION `
    --subscription $SUBSCRIPTION_ID `

# create the key vault
az keyvault create `
    --name $KEY_VAULT_NAME `
    --resource-group $RESOURCE_GROUP `
    --location $LOCATION `
    --subscription $SUBSCRIPTION_ID `
    --enabled-for-template-deployment true `

# retrieve the user principal name
$USER_PRINCIPAL_NAME = az ad signed-in-user show `
    --query userPrincipalName `
    --output tsv
echo $USER_PRINCIPAL_NAME

# setup the policies for the user principal or other user/system principals
az keyvault set-policy `
    --name $KEY_VAULT_NAME `
    --upn $USER_PRINCIPAL_NAME `
    --secret-permissions set get delete list `
    --subscription $SUBSCRIPTION_ID

# generate a secret
$PASSWORD=$(openssl rand -base64 32)
echo $PASSWORD

# add a secret to the key vault
az keyvault secret set `
    --vault-name $KEY_VAULT_NAME `
    --name "myPassword" `
    --value $PASSWORD `
    --subscription $SUBSCRIPTION_ID

# get/show the secret 
az keyvault secret show `
    --vault-name $KEY_VAULT_NAME `
    --name "myPassword" `
    --query value `
    --output tsv `
    --subscription $SUBSCRIPTION_ID
