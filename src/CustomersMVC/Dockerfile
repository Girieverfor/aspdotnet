FROM mcr.microsoft.com/dotnet/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build
WORKDIR /src
COPY src/CustomersMVC/CustomersMVC.csproj src/CustomersMVC/
COPY src/CustomersDataModels/CustomersDataModels.csproj src/CustomersDataModels/
COPY src/RequestCorrelation/RequestCorrelation.csproj src/RequestCorrelation/
COPY src/ApplicationInsightsInitializers/ApplicationInsightsInitializers.csproj src/ApplicationInsightsInitializers/
RUN dotnet restore src/CustomersMVC/CustomersMVC.csproj
COPY . .
WORKDIR /src/src/CustomersMVC
RUN dotnet build CustomersMVC.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish CustomersMVC.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CustomersMVC.dll"]
