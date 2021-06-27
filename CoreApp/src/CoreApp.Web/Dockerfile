#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["CoreApp.Web/CoreApp.Web.csproj", "CoreApp.Web/"]
RUN dotnet restore "CoreApp.Web/CoreApp.Web.csproj"
COPY . .
WORKDIR "/src/CoreApp.Web"
RUN dotnet build "CoreApp.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CoreApp.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CoreApp.Web.dll"]