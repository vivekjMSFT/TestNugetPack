# TestNugetPack
Test Repo to reproduce Nuget Pack dependency issue

I am looking to create a single nuget package out of multiple .csproj.  

Ex: I have two .csproj, one of them having dependency on other external packages such as NewtonSoft.

    dotnet new classlib -o ClassLibrary1
    dotnet new classlib -o ClassLibrary2
    cd ClassLibrary1
    dotnet add package Newtonsoft.Json

I am looking to publish a single nuget package which contains both ClassLibrary1.dll and ClassLibrary2.dll and resulting .nuspec have dependency Newtonsoft.Json listed.

I tried doing something like this: Created a dummy .csproj and added references to ClassLibrary1 & 2 and created a nuget package with -IncludeReferencedProjects: Ex:-

    dotnet new classlib -o dummyNuget
    dotnet add reference ClassLibrary1.csproj
    dotnet add reference ClassLibrary2.csproj
    nuget pack dummyNuget.csproj -IncludeReferencedProjects

it produces below .nuspec file , missing the NewtonSoft Dependency. 
    
```
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
  <metadata>
    <id>dummynuget</id>
    <version>1.0.0</version>
    <authors></authors>
    <description>Description</description>
    <dependencies />
  </metadata>
</package>
```

Any ideas? how to create a single nuget package with -IncludeReferencedProjects and all the dependencies listed.

I know common approach would be to first combine the source files into a single project and thus use dotnet pack to publish a single package but lets say that option is not available easily due to cross team dependencies.


