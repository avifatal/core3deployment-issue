FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["TestCloudRun.csproj", "TestCloudRun/"]
RUN dotnet restore "TestCloudRun/TestCloudRun.csproj"
COPY . .
WORKDIR "/src/TestCloudRun"
RUN dotnet build "TestCloudRun.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestCloudRun.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestCloudRun.dll"]                