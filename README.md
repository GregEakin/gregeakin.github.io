# Gregory's Web Page

This is Gregory's home page.
it's the backing website for my URL: [https://www.eakin.dev](https://www.eakin.dev)

## Steps
```shell
mkdir gregeakin.github.io
cd gregeakin.github.io
dotnet new sln -o . -n gregeakin.github.io
dotnet new globaljson --sdk-version 9.0.101 --output .
dotnet new blazorwasm --output GitHubPages
dotnet sln . add GitHubPages
.\gregeakin.github.io.sln
```

## Author
:t-rex: [Gregory Eakin](https://www.linkedin.com/in/gregeakin)
