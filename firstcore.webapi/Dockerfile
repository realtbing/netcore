FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY firstcore.sln ./
COPY firstcore.webapi/firstcore.webapi.csproj firstcore.webapi/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/firstcore.webapi
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "firstcore.webapi.dll"]
