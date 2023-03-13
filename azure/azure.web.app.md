# Azure Web App 

# Azure Web App - Command Line Interface (CLI)

step1. Create a group of resources

```powershell
# login to Azure
az login
# list the subscriptions
az account list --output table
# or 
az account list --query "[].{name}" --output tsv
# or search for a certain subscription
az account list --query "[?contains(name, 'spo')].{name}" --output tsv

# set the subscription
az account set --subscription "Visual Studio Enterprise"

az group create --name myResourceGroup --location westeurope
```

step2. Create a web app

```powershell
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name myUniqueAppServiceName --runtime "DOTNETCORE|6.0"
```

step3. Deploy code to the web app


```powershell

# get all the subscriptions (names)
az account list --query "[].{name: name, id: id}"

# get all the resource groups (names)
az group list --query "[].{name: name, id: id}"  

# get all the web apps (names) - in a specific resource group
az resource list --query "[?resourceGroup=='example-web-app'].{name: name, id: id}"

az webapp deploy --subscription  "c3407f72-80bd-4627-ae31-d07cfe8adcb7" --resource-group  "example-web-app" --name "lucian1" --src-path "./bin/Debug/net6.0/publish"
```
