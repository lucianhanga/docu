# Function Applications

## What is a Function App?

A **Function App** is a serverless compute service that runs your code in response to events or on a schedule. You can write your code in any of the languages supported by Azure Functions, including C#, F#, JavaScript, PowerShell, and Python. You can also use a pre-built function template to get started quickly.

## Create a Function App

Create a function app using the Power Shell command `func` form **Azure Functions Core Tools**.

### Create a function triggered by HTTP

```powershell
# Creat a new function app project
func init MyFunctionApp --worker-runtime python --force

# Create a new function using a template for HTTP trigger
func new --name MyHttpFunction --template "HTTP trigger" --language Python

# build the function app
func start --build
```

test the function app

```powershell
# install the httpie tool
dotnet tool install -g Microsoft.dotnet-httprepl
# or if python is installed
pip install httpie

# test the function app
httprepl http://localhost:7071/api/MyHttpFunction
```

### Create a function triggered by a timer

```powershell
# Creat a new function app project
func init MyFunctionApp --worker-runtime python --force

# Create a new function using a template for timer trigger
func new --name MyTimerFunction --template "Timer trigger" --language Python
```

### Create a function triggered by HTTP which accesses a blob storage

```powershell
# install the blob storage extension
func extensions install --package Microsoft.Azure.WebJobs.Extensions.Storage --version 5.0.1

# Creat a new function app project
func init MyFunctionApp --worker-runtime python --force

# Create a new function using a template for HTTP trigger
func new --template "HTTP trigger" --name "GetSettingInfo"
```

the function code

```csharp

using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
public static class GetSettingInfo
{
    [FunctionName("GetSettingInfo")]
    public static IActionResult Run(
        [HttpTrigger("GET")] HttpRequest request,
        [Blob("content/settings.json")] string json)
        => new OkObjectResult(json);
}
```

publish the function app.


```powershell
az login
func azure functionapp publish <function-app-name>
```
