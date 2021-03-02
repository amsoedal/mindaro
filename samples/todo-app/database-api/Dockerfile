FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
LABEL io.k8s.display-name="database-api" \
      io.k8s.description="database-api service from the todoapp" \
      io.openshift.expose-services="8080:http"

EXPOSE 8080
ENV ASPNETCORE_URLS=http://*:8080

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["databaseApi.csproj", ""]
RUN dotnet restore "./databaseApi.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "databaseApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "databaseApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "databaseApi.dll"]