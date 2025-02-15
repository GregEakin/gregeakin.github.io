FROM nginx:alpine AS base
#USER $APP_UID
WORKDIR /var/www/web
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["GitHubPages/GitHubPages.csproj", "GitHubPages/"]
RUN dotnet workload install wasm-tools
RUN dotnet restore "./GitHubPages/GitHubPages.csproj"
COPY . .
WORKDIR "/src/GitHubPages"
RUN dotnet build "./GitHubPages.csproj" -c $BUILD_CONFIGURATION --no-restore --nologo -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN . /etc/os-release \
    && case $ID in \
        alpine) apk add --no-cache python3 ;; \
        debian | ubuntu) apt-get update \
            && apt-get install -y --no-install-recommends python3 \
            && rm -rf /var/lib/apt/lists/* ;; \
        mariner) tdnf install -y python3 \
            && tdnf clean all ;; \
        esac \
    && dotnet workload install --skip-manifest-update wasm-tools
RUN dotnet publish "./GitHubPages.csproj" -c $BUILD_CONFIGURATION --no-restore --no-build --nologo -o /app/publish /p:UseAppHost=false

# RUN docker build -t vim3.lab.eakin.wtf:5000/standalone:latest .
# RUN docker run -d --rm -p 5040:80 --name standalone vim3.lab.eakin.wtf:5000/standalone:latest

FROM base AS final
WORKDIR /var/www/web
COPY --from=publish /app/publish/wwwroot .
COPY ["GitHubPages/nginx.conf", "/etc/nginx/nginx.conf"]
EXPOSE 80
EXPOSE 443
