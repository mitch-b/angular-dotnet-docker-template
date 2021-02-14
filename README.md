# Angular and .NET Web API Docker Template

* Docker multi-stage build and runtime
* Angular 11
* .NET 5 Web API
* _todo: GitHub actions_

## Get Started

#### PowerShell

[Download PowerShell](https://github.com/PowerShell/PowerShell/releases)

```powershell
# do not change this
$TemplateName = "web-template"; $TemplateNamespace = "WebTemplate"

# you change these!
$NewProjectName = "my-new-app"
$NewProjectNamespace = "MyNewApp"

git clone https://github.com/mitch-b/angular-dotnet-docker-template $NewProjectName
cd $NewProjectName

# todo ... file renames from template
```

## Building / Running

```powershell
cd $NewProjectName/src
docker-compose up --build

# open UI at http://localhost:8876
# open API at http://localhost:8877
```