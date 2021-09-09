#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

                              #asp.netcore 版本
FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 1233
#暴露端口

                               #.netcore 版本
FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
#项目名/项目名.csproj      项目名/
COPY ["dotnetcoreforazuredevops/dotnetcoreforazuredevops.csproj", "dotnetcoreforazuredevops/"]
RUN dotnet restore "dotnetcoreforazuredevops/dotnetcoreforazuredevops.csproj"
COPY . .
WORKDIR "/src/dotnetcoreforazuredevops"
RUN dotnet build "dotnetcoreforazuredevops.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnetcoreforazuredevops.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
#项目名.dll
ENTRYPOINT ["dotnet", "dotnetcoreforazuredevops.dll"]
