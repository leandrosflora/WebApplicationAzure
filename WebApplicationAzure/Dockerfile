FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["WebApplicationAzure/WebApplicationAzure.csproj", "WebApplicationAzure/"]
RUN dotnet restore "WebApplicationAzure/WebApplicationAzure.csproj"
COPY . .
WORKDIR "/src/WebApplicationAzure"
RUN dotnet build "WebApplicationAzure.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApplicationAzure.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplicationAzure.dll"]