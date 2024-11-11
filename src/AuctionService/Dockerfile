# Use .NET SDK for build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy solution and all project files
COPY Carsties.sln .
COPY src/AuctionService/AuctionService.csproj src/AuctionService/
COPY src/SearchService/SearchService.csproj src/SearchService/
COPY src/GatewayService/GatewayService.csproj src/GatewayService/
COPY src/IdentityService/IdentityService.csproj src/IdentityService/
COPY src/Contracts/Contracts.csproj src/Contracts/

# Restore dependencies for the solution
RUN dotnet restore

# Copy the entire source folder to include all code files
COPY src/ src/
WORKDIR /app/src/AuctionService
RUN dotnet publish -c Release -o /app/publish

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "AuctionService.dll"]
