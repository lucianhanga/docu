# Event Grid CLI



```powershell

# generate a random number between 1 and 100
$randomNumber = Get-Random -Minimum 1 -Maximum 100
$mylocation = "westus"
# define the topic name
$myTopicName = "az204-myTopic-$randomNumber"
echo $myTopicName
$mySiteName = "az204-mySite-$randomNumber"
echo $mySiteName
$mySiteURL="https://$mySiteName.azurewebsites.net"
echo $mySiteURL


# create a resource group
az group create --name az204-evgrid-rg --location $mylocation

# enable an Event Grid resource provider
az provider register --namespace Microsoft.EventGrid
az provider show --namespace Microsoft.EventGrid --query "registrationState"

# create a custom topic
az eventgrid topic create --name $myTopicName `
    --location $myLocation `
    --resource-group az204-evgrid-rg `
```

## Create an endpoint for the event message

Before subscribing to the custom topic, we need to create the endpoint for the event message. Typically, the endpoint takes actions based on the event data. The script below uses a pre-built web app that displays the event messages. The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub. It also generates a unique name for the site.
  
```powershell
az deployment group create `
    --resource-group az204-evgrid-rg `
    --template-uri "https://raw.githubusercontent.com/Azure-Samples/azure-event-grid-viewer/main/azuredeploy.json" `
    --parameters siteName=$mySiteName hostingPlanName=viewerhost `

echo "Your web app URL: ${mySiteURL}"
```

## Subscribe to the custom topic

```powershell
$endpoint="${mySiteURL}/api/updates"

# get the subscription id
$subId=$(az account show | jq -r '.id')
echo $subId

# subscribe to the topic
az eventgrid event-subscription create `
    --source-resource-id "/subscriptions/$subId/resourceGroups/az204-evgrid-rg/providers/Microsoft.EventGrid/topics/$myTopicName" `
    --name az204ViewerSub `
    --endpoint $endpoint `
```

## Publish an event to the custom topic

```powershell
# get the topic endpoint
$topicEndpoint = az eventgrid topic show `
      --name $myTopicName `
       --resource-group az204-evgrid-rg `
       --query "endpoint" `
       --output tsv
echo $topicEndpoint

# get the topic key
$topicKey = az eventgrid topic key list `
      --name $myTopicName `
      --resource-group az204-evgrid-rg `
      --query "key1" `
      --output tsv
echo $topicKey

```

## Publish an event to the custom topic

```powershell
# define an event

# current date 
$eventTime = Get-Date -Format "yyyy-MM-ddTHH:mm:sszzz"
$eventID = [guid]::NewGuid().ToString()

# define the event
$event = @{
    id = $eventID
    eventType = "recordInserted"
    subject = "myapp/vehicles/motorcycles"
    eventTime = $eventTime
    dataVersion = "1.0"
    data = @{
      "make" = "Contoso"
      "model" = "Monster"
    }
} | ConvertTo-Json

# make an array of events
$events = "[ $event ]"
echo $events

# publish the event
curl -X POST -H "aeg-sas-key: $topicKey" -d "$events" $topicEndpoint



