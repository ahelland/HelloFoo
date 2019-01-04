FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["FooBackend/FooBackend.csproj", "FooBackend/"]
RUN dotnet restore "FooBackend/FooBackend.csproj"
COPY . .
WORKDIR "/src/FooBackend"
RUN dotnet build "FooBackend.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "FooBackend.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "FooBackend.dll"]