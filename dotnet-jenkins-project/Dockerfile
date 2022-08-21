#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dotnet-jenkins-project/dotnet-jenkins-project.csproj", "dotnet-jenkins-project/"]
RUN dotnet restore "dotnet-jenkins-project/dotnet-jenkins-project.csproj"
COPY . .
WORKDIR "/src/dotnet-jenkins-project"
RUN dotnet build "dotnet-jenkins-project.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet-jenkins-project.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet-jenkins-project.dll"]