# How to publish a WebApp from Visual Studio

## setup the application in azure using the CLI

```powershell
# login to Azure
az login

# create a resource group
az group create `
    --name lh-web-app-gr `
    --location westeurope `

# create a app service plan
az appservice plan create `
    --name lh-web-app-plan `
    --resource-group lh-web-app-gr `
    --sku F1 `
    --location westeurope `

# list runtimes 
az webapp list-runtimes

# create a web app
az webapp create `
    --name lh-web-app-2022 `
    --resource-group lh-web-app-gr `
    --plan lh-web-app-plan `
    --runtime "dotnet:6" `

# list all the applications available on  Azure
az webapp list `
    --query "[].{hostName: defaultHostName, state: state}" `
    --output tsv

```

## setup the application in azure using the powershell

```powershell
# login to Azure
Connect-AzAccount
# check out the available subscriptions
Get-AzSubscription
# check out the default subscription
Get-AzContext

# create a resource group
New-AzResourceGroup `
    -Name lh-web-app2-gr `
    -Location westeurope `

# create a app service plan
New-AzAppServicePlan `
    -Name lh-web-app2-plan `
    -ResourceGroupName lh-web-app2-gr `
    -Location westeurope `
    -Tier Free `

# create a web app
New-AzWebApp `
    -Name lh-web-app2-2022 `
    -ResourceGroupName lh-web-app2-gr `
    -AppServicePlan lh-web-app2-plan `
    -Runtime "dotnet:6" `

# get hte config of the web app
config = Get-AzWebApp `
    -Name lh-web-app2-2022 `
    -ResourceGroupName lh-web-app2-gr

# set the runtime version
config.properties.netFrameworkVersion = "v6.0"
# set the runtime stack


```




