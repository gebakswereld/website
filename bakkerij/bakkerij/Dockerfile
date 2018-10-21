FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY bakkerij/bakkerij.csproj bakkerij/
RUN dotnet restore bakkerij/bakkerij.csproj
COPY . .
WORKDIR /src/bakkerij
RUN dotnet build bakkerij.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish bakkerij.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "bakkerij.dll"]
