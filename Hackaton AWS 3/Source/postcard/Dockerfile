FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Hackaton AWS 3/Source/postcard/postcard.csproj", "Hackaton AWS 3/Source/postcard/"]
RUN dotnet restore "Hackaton AWS 3/Source/postcard/postcard.csproj"
COPY . .
WORKDIR "/src/Hackaton AWS 3/Source/postcard"
RUN dotnet build "postcard.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "postcard.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "postcard.dll"]
