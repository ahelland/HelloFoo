#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine AS build
WORKDIR /src
COPY ["FooBackend/FooBackend.csproj", "FooBackend/"]
RUN dotnet restore "FooBackend/FooBackend.csproj"
COPY . .
WORKDIR "/src/FooBackend"
RUN dotnet build "FooBackend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FooBackend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FooBackend.dll"]