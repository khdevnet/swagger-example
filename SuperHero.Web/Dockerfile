FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["SuperHero.Web/SuperHero.Web.csproj", "SuperHero.Web/"]
RUN dotnet restore "SuperHero.Web/SuperHero.Web.csproj"
COPY . .
WORKDIR "/src/SuperHero.Web"
RUN dotnet build "SuperHero.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SuperHero.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SuperHero.Web.dll"]