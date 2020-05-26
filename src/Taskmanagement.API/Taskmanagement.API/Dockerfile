#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Taskmanagement.API/Taskmanagement.API.csproj", "Taskmanagement.API/"]
RUN dotnet restore "Taskmanagement.API/Taskmanagement.API.csproj"
COPY . .
WORKDIR "/src/Taskmanagement.API"
RUN dotnet build "Taskmanagement.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Taskmanagement.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Taskmanagement.API.dll"]