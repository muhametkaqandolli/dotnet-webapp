#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["dotnet-webapp/dotnet-webapp.csproj", "dotnet-webapp/"]
RUN dotnet restore "dotnet-webapp/dotnet-webapp.csproj"
COPY . .
WORKDIR "/src/dotnet-webapp"
RUN dotnet build "dotnet-webapp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet-webapp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet-webapp.dll"]