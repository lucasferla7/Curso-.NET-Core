#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/ITDeveloper.CursoAspNetCore.Presentation/ITDeveloper.CursoAspNetCore.Presentation.csproj", "src/ITDeveloper.CursoAspNetCore.Presentation/"]
RUN dotnet restore "src/ITDeveloper.CursoAspNetCore.Presentation/ITDeveloper.CursoAspNetCore.Presentation.csproj"
COPY . .
WORKDIR "/src/src/ITDeveloper.CursoAspNetCore.Presentation"
RUN dotnet build "ITDeveloper.CursoAspNetCore.Presentation.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ITDeveloper.CursoAspNetCore.Presentation.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ITDeveloper.CursoAspNetCore.Presentation.dll"]