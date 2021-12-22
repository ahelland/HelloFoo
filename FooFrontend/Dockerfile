FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine AS build
WORKDIR /src
COPY FooFrontend/FooFrontend.csproj FooFrontend/
RUN dotnet restore FooFrontend/FooFrontend.csproj
COPY . .
WORKDIR /src/FooFrontend
RUN dotnet build FooFrontend.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish FooFrontend.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "FooFrontend.dll"]