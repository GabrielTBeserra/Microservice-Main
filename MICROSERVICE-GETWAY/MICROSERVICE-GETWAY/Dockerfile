#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MICROSERVICE-GETWAY/MICROSERVICE-GETWAY.csproj", "MICROSERVICE-GETWAY/"]
RUN dotnet restore "MICROSERVICE-GETWAY/MICROSERVICE-GETWAY.csproj"
COPY . .
COPY /MICROSERVICE-GETWAY/ocelot.json ./ocelot.json
WORKDIR "/src/MICROSERVICE-GETWAY"
RUN dotnet build "MICROSERVICE-GETWAY.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MICROSERVICE-GETWAY.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MICROSERVICE-GETWAY.dll"]