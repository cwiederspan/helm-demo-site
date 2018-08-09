FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Helm.Site/Helm.Site.csproj Helm.Site/
RUN dotnet restore Helm.Site/Helm.Site.csproj
COPY . .
WORKDIR /src/Helm.Site
RUN dotnet build Helm.Site.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Helm.Site.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Helm.Site.dll"]
