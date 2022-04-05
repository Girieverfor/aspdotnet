FROM mcr.microsoft.com/dotnet/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build
WORKDIR /src
COPY . .
COPY /src/CustomersAPI/CustomersAPI.csproj src/CustomersAPI/
COPY /src/CustomersDataModels/CustomersDataModels.csproj src/CustomersDataModels/
COPY /src/RequestCorrelation/RequestCorrelation.csproj src/RequestCorrelation/
COPY /src/ApplicationInsightsInitializers/ApplicationInsightsInitializers.csproj src/ApplicationInsightsInitializers/
RUN dotnet restore src/CustomersAPI/CustomersAPI.csproj
COPY . .
WORKDIR /src/src/CustomersAPI
RUN dotnet build CustomersAPI.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish CustomersAPI.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CustomersAPI.dll"]
