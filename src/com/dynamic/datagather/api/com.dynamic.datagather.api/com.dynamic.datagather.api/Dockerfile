#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["com.dynamic.datagather.api/com.dynamic.datagather.api.csproj", "com.dynamic.datagather.api/"]
RUN dotnet restore "com.dynamic.datagather.api/com.dynamic.datagather.api.csproj"
COPY . .
WORKDIR "/src/com.dynamic.datagather.api"
RUN dotnet build "com.dynamic.datagather.api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "com.dynamic.datagather.api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "com.dynamic.datagather.api.dll"]