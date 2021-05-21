#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["OPA.API/OPA.API.csproj", "OPA.API/"]
RUN dotnet restore "OPA.API/OPA.API.csproj"
COPY . .
WORKDIR "/src/OPA.API"
RUN dotnet build "OPA.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OPA.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OPA.API.dll"]
