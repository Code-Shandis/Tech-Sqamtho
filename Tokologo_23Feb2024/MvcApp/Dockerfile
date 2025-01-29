FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 8084
EXPOSE 443  

# Use .NET 6.0 SDK for build and restore
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY "MvcApp.csproj" .
RUN dotnet restore "MvcApp.csproj"
COPY . .
RUN dotnet build . -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MvcApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MvcApp.dll"]