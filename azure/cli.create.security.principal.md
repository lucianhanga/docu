# Create a Security Principal for a Group

## CLI on powershell

```powershell
# login to Azure
az login

# get the subscriptions 
az account list --output table

# define the subscription variable
$SUBSCRIPTION_ID = "9b79def9-4b73-4eac-886d-8ce529aacacd"
echo $SUBSCRIPTION_ID

# list all groups in a subscription
az group list `
  --subscription $SUBSCRIPTION_ID `
  --output table

# define the variables
$RESOURCE_GROUP = "rg-az400-eshoponweb-lucianhanga"
echo $RESOURCE_GROUP

# create the group
az group create `
    --name $RESOURCE_GROUP `
    --subscription $SUBSCRIPTION_ID `
    --location westeurope `

# list all the groups
az group list `
    --subscription $SUBSCRIPTION_ID `
    --output table


# create a security principal with contributor access for the group
$SECURITY_PRINCIPAL_NAME = "GH-Action-eshoponweb"
echo $SECURITY_PRINCIPAL_NAME
az ad sp create-for-rbac `
  --name $SECURITY_PRINCIPAL_NAME `
  --role contributor `
  --scopes /subscriptions/${SUBSCRIPTION_ID}/resourceGroups/${RESOURCE_GROUP} `
  --sdk-auth

# !!! IMPORTANT
# save the output into a notepad file for later use
# the clientSecret is only available _once_

# get the security principal id
az ad sp list `
  --display-name $SECURITY_PRINCIPAL_NAME `
  --query "[].appId" `
  --output tsv

# save the output into a variable
$SECURITY_PRINCIPAL_ID = az ad sp list `
  --display-name $SECURITY_PRINCIPAL_NAME `
  --query "[].appId" `
  --output tsv
echo $SECURITY_PRINCIPAL_ID

# get the security principal clientID
$SP_CLIENT_ID = az ad sp list `
  --display-name $SECURITY_PRINCIPAL_NAME `
  --query "[].appId" `
  --output tsv
echo $SP_CLIENT_ID

# get the security principal tenantID
$SP_TENANT_ID = az ad sp list `
  --display-name $SECURITY_PRINCIPAL_NAME `
  --query "[].appOwnerOrganizationId" `
  --output tsv
echo $SP_TENANT_ID

# delete the security principal
az ad sp delete `
  --id $SECURITY_PRINCIPAL_ID
  
# remove the group
az group delete `
    --name $RESOURCE_GROUP `
    --subscription $SUBSCRIPTION_ID `
    --yes `
    --no-wait `

