# Gregory's Web Page

This is Gregory's home page.
it's the backing website for my URL: [https://www.eakin.dev](https://www.eakin.dev)

## Project Creation
```shell
mkdir gregeakin.github.io
cd gregeakin.github.io
dotnet new sln -o . -n gregeakin.github.io
dotnet new globaljson --sdk-version 9.0.101 --output .
dotnet new blazorwasm --output GitHubPages
dotnet sln . add GitHubPages

dotnet publish -c Release -o release --nologo -r linux-x64 -p:PublishTrimmed=true
.\gregeakin.github.io.sln
```

## Docker steps
```shell
docker build -t githubpages -f GitHubPages/Dockerfile .
docker tag githubpages vim3.lab.eakin.wtf:5000/githubpages:latest
docker push vim3.lab.eakin.wtf:5000/githubpages:latest
docker run -d -p 5061:8081 -p 5060:8080 --name githubpages vim3.lab.eakin.wtf:5000/githubpages:latest
```

## Author
:t-rex: [Gregory Eakin](https://www.linkedin.com/in/gregeakin)
