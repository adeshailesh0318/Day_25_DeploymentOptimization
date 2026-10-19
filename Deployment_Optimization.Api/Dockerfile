# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

COPY ["Deployment_Optimization.Api.csproj", "./"]
RUN dotnet restore "Deployment_Optimization.Api.csproj"

COPY . .
RUN dotnet publish "Deployment_Optimization.Api.csproj" \
    -c Release \
    -o /app/publish \
    --no-restore

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

COPY --from=build /app/publish .

ENV ASPNETCORE_HTTP_PORTS=8080
EXPOSE 8080

ENTRYPOINT ["dotnet", "Deployment_Optimization.Api.dll"]