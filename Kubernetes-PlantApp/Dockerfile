FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Kubernetes-PlantApp.csproj", "."]
RUN dotnet restore "Kubernetes-PlantApp.csproj"
COPY . .
RUN dotnet build "Kubernetes-PlantApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Kubernetes-PlantApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Kubernetes-PlantApp.dll"]
