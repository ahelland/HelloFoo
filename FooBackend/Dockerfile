FROM mcr.microsoft.com/dotnet/aspnet:5.0-alpine AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-alpine AS build
WORKDIR /src
COPY FooBackend/FooBackend.csproj FooBackend/
RUN dotnet restore FooBackend/FooBackend.csproj
COPY . .
WORKDIR /src/FooBackend
RUN dotnet build FooBackend.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish FooBackend.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "FooBackend.dll"]
