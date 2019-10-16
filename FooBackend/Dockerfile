FROM mcr.microsoft.com/dotnet/core/runtime:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
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
