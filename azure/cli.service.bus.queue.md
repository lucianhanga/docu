# Service Bus Queue

## Create a queue

```powershell
# login to Azure
az login

# create the group
az group create --name sbq1 --location westeurope

# create the namespace
$RANDOM = Get-Random -Minimum 1000 -Maximum 9999
$NAMESPACE_NAME="sbq1lucian-$RANDOM"
echo $NAMESPACE_NAME
az servicebus namespace create `
      --resource-group sbq1 `
      --name $NAMESPACE_NAME `
      --location westeurope `

# create the queue
az servicebus queue create `
      --resource-group sbq1 `
      --namespace-name $NAMESPACE_NAME `
      --name sbq1lucian `
      --verbose `

```
