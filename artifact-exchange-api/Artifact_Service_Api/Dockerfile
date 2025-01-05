FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Устанавливаем рабочий каталог в /app
WORKDIR /app

# Копируем только csproj файл и выполняем restore.
COPY *.csproj ./  
RUN df -h
RUN dotnet restore Artifact_Service_Api.csproj 

# Копируем остальные файлы.
COPY . .
RUN df -h
# Собираем проект.
RUN dotnet build "Artifact_Service_Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Artifact_Service_Api.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .

EXPOSE 80
ENTRYPOINT ["dotnet", "Artifact_Service_Api.dll"]