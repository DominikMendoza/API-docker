FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ZenDriver.API/ZenDriver.API.csproj", "ZenDriver.API/"]
RUN dotnet restore "ZenDriver.API/ZenDriver.API.csproj"
COPY . .
WORKDIR "/src/ZenDriver.API"
RUN dotnet build "ZenDriver.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ZenDriver.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ZenDriver.API.dll"]
