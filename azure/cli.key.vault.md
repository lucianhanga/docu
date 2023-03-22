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
