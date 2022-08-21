#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
COPY *.csproj .
COPY . ./
RUN dotnet publish --no-restore -c Release -o out
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from-build-env /app/out .
ENTRYPOINT ["dotnet","dotnet-jenkins-project.dll"]