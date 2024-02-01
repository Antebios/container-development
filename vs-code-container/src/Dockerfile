FROM mcr.microsoft.com/dotnet/sdk:7.0 AS installer-env

# COPY . /src/dotnet-web-app
# RUN cd /src/dotnet-web-app && \
#     mkdir -p /home/site/wwwroot && \
#     dotnet restore vs-code-container.csproj && \
#     dotnet publish vs-code-container.csproj --output /home/site/wwwroot

WORKDIR /source
COPY . .
RUN dotnet restore
# -ucr
RUN dotnet publish -c release -o /app --no-restore

# To enable ssh & remote debugging on app service change the base image to the one below
# # FROM mcr.microsoft.com/azure-functions/dotnet-isolated:3.0-dotnet-isolated7.0-appservice
# FROM mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated7.0
# ENV AzureWebJobsScriptRoot=/home/site/wwwroot \
#     AzureFunctionsJobHost__Logging__Console__IsEnabled=true

FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=installer-env ["/app", "/app"]
# USER ContainerUser
ENTRYPOINT ["dotnet","/app/vs-code-container.dll"]
