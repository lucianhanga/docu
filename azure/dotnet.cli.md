# dotnet command

The dotnet command has two functions:

- It provides commands for working with .NET projects.
For example, `dotnet build` builds a project.

- It runs .NET applications.
You specify the path to an application .dll file to run the application. To run the application means to find and execute the entry point, which in the case of **console apps** is the `Main` method. For example, `dotnet myapp.dll` runs the myapp application. 

## display environment information

`--list-runtimes` - Prints out a list of the installed .NET runtimes. An x86 version of the SDK lists only x86 runtimes, and an x64 version of the SDK lists only x64 runtimes.

`--list-sdks` - Prints out a list of the installed .NET SDKs.

## dotnet commands

`dotnet build`  Builds a .NET application.
`dotnet clean`  Clean build outputs.
`dotnet exec`   Runs a .NET application.
`dotnet new`    Initializes a C# or F# project for a given template.
`dotnet publish` Publishes a .NET framework-dependent or self-contained application.
`dotnet restore` Restores the dependencies for a given application.
`dotnet run` Runs the application from source.
`dotnet sdk check` Shows up-to-date status of installed SDK and Runtime versions.
`dotnet test` Runs tests using a test runner.

`dotnet add package` Adds a package reference to a project.
`dotnet remove package` Removes a package reference from a project.

`dotnet nuget delete` Deletes a package from a NuGet server.
`dotnet nuget locals` Lists and manages local NuGet resources.
`dotnet nuget add source` Adds a NuGet package source.
`dotnet nuget disable source` Disables a NuGet package source.
`dotnet nuget enable source` Enables a NuGet package source.
`dotnet nuget list source` Lists all NuGet package sources.
`dotnet nuget remove source` Removes a NuGet package source.
`dotnet nuget update source` Updates a NuGet package source.

tools are console applications that are installed from NuGet packages.
`dotnet tool install` Installs a tool for use on the command line.
`dotnet tool list` Lists the tools installed globally.
`dotnet tool restore` Restores the tools for a given application.
`dotnet tool search` Searches for tools on NuGet.

## other commands

`dev-certs` - Creates and manages development certificates.
`ef` - Entity Framework Core command-line tools.
`user-secrets` - Stores and retrieves user secrets.
`watch` - Runs a .NET application when source files change.

## examples

`dotnet new console -o myApp` - Creates a new console application in the myApp directory.
`dotnet build` - Builds the application.
`dotnet exec myApp.dll` - Runs the application.

