#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Okta.Demo.Web.App/Okta.Demo.Web.App.csproj", "Okta.Demo.Web.App/"]
RUN dotnet restore "Okta.Demo.Web.App/Okta.Demo.Web.App.csproj"
COPY . .
WORKDIR "/src/Okta.Demo.Web.App"
RUN dotnet build "Okta.Demo.Web.App.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Okta.Demo.Web.App.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Okta.Demo.Web.App.dll"]