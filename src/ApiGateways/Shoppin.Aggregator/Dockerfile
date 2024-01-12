#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ApiGateways/Shoppin.Aggregator/Shoppin.Aggregator.csproj", "ApiGateways/Shoppin.Aggregator/"]
RUN dotnet restore "ApiGateways/Shoppin.Aggregator/Shoppin.Aggregator.csproj"
COPY . .
WORKDIR "/src/ApiGateways/Shoppin.Aggregator"
RUN dotnet build "Shoppin.Aggregator.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Shoppin.Aggregator.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Shoppin.Aggregator.dll"]
