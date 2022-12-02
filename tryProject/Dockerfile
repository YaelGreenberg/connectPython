#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["tryProject/tryProject.csproj", "tryProject/"]
RUN dotnet restore "tryProject/tryProject.csproj"
COPY . .
WORKDIR "/src/tryProject"
RUN dotnet build "tryProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "tryProject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "tryProject.dll"]