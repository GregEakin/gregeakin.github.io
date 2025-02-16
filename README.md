# Gregory's Web Page

This is Gregory's home page.
it's the backing website for my URL: [https://www.eakin.dev](https://www.eakin.dev)

## Project Creation
```shell
mkdir gregeakin.github.io
cd gregeakin.github.io
dotnet new sln -o . -n gregeakin.github.io
dotnet new globaljson --output . --sdk-version 9.0.200 --roll-forward latestFeature
dotnet new blazorwasm --output GitHubPages
dotnet sln . add GitHubPages

dotnet workload install wasm-tools
dotnet tool install --global microsoft.web.librarymanager.cli
dotnet restore
dotnet build ./GitHubPages/GitHubPages.csproj --configuration Release --no-restore
dotnet publish ./GitHubPages/GitHubPages.csproj -c:Release -o dist/Web -p:GHPages=true -p:PublishTrimmed=true -p:UseAppHost=false --nologo --no-restore --no-build

.\gregeakin.github.io.sln
```

## Author
:t-rex: [Gregory Eakin](https://www.linkedin.com/in/gregeakin)
