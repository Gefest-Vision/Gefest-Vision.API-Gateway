FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Gefest-Vision.Gateway/Gefest-Vision.Gateway.csproj", "Gefest-Vision.Gateway/"]
RUN dotnet restore "Gefest-Vision.Gateway/Gefest-Vision.Gateway.csproj"
COPY . .
WORKDIR "/src/Gefest-Vision.Gateway"
RUN dotnet build "Gefest-Vision.Gateway.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Gefest-Vision.Gateway.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Gefest-Vision.Gateway.dll"]
