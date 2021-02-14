# Angular and .NET Web API Docker Template

* Docker multi-stage build and runtime
* Angular 11
* .NET 5 Web API
* _todo: GitHub actions_

## Get Started

Copy the entire script into your shell and run:

#### PowerShell

[Download PowerShell](https://github.com/PowerShell/PowerShell/releases)

```powershell
# you change these!
$NewProjectName = "my-new-app"
$NewProjectNamespace = "MyNewApp"

# do not change this
$TemplateName = "web-template"
$TemplateNamespace = "WebTemplate"

git clone https://github.com/mitch-b/angular-dotnet-docker-template $NewProjectName
cd $NewProjectName

$files = gci . -Recurse -Include "*.cs","*.json","*.ts","*.csproj","*.yml","Dockerfile",".*ignore" | select FullName
$files | % {
  (gc $_.FullName).replace($TemplateName,$NewProjectName).replace($TemplateNamespace,$NewProjectNamespace) | Set-Content $_.FullName
}
gci -Filter "$($TemplateNamespace)*" -Recurse | rni -NewName {$_.name -Replace $TemplateNamespace,$NewProjectNamespace }

# remove existing repo and re-init
rm .git -Force -Recurse
git init
git add .
git commit -m "Initial commit"

git status

```

## Building / Running

```powershell
cd $NewProjectName/src
docker-compose up --build

# open UI at http://localhost:8876
# open API at http://localhost:8877
```