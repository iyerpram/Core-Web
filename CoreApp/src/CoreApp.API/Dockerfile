#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["CoreApp.API/CoreApp.API.csproj", "CoreApp.API/"]
RUN dotnet restore "CoreApp.API/CoreApp.API.csproj"
COPY . .
WORKDIR "/src/CoreApp.API"
RUN dotnet build "CoreApp.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CoreApp.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CoreApp.API.dll"]