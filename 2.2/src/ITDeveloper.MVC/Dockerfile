#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/ITDeveloper.MVC/ITDeveloper.MVC.csproj", "src/ITDeveloper.MVC/"]
RUN dotnet restore "src/ITDeveloper.MVC/ITDeveloper.MVC.csproj"
COPY . .
WORKDIR "/src/src/ITDeveloper.MVC"
RUN dotnet build "ITDeveloper.MVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ITDeveloper.MVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ITDeveloper.MVC.dll"]