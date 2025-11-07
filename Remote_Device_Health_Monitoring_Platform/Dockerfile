# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 5000

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy .csproj from the project folder (relative to Dockerfile)
COPY Remote_Device_Health_Monitoring_Platform/*.csproj ./Remote_Device_Health_Monitoring_Platform/

# Set working directory to project
WORKDIR /src/Remote_Device_Health_Monitoring_Platform

# Restore
RUN dotnet restore

# Copy source
COPY Remote_Device_Health_Monitoring_Platform/. .

# Publish
RUN dotnet publish -c Release -o /app/out --no-restore

# Final stage
FROM base AS final
WORKDIR /app
COPY --from=build /app/out ./
ENTRYPOINT ["dotnet", "Remote_Device_Health_Monitoring_Platform.dll"]