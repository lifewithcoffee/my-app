FROM mcr.microsoft.com/dotnet/aspnet:6.0-focal AS base
WORKDIR /app
EXPOSE 81

ENV ASPNETCORE_URLS=http://+:81

FROM mcr.microsoft.com/dotnet/sdk:6.0-focal AS build
WORKDIR /src
#COPY ["src/svc2-blazorserver/svc2-blazorserver.csproj", "src/svc2-blazorserver/"]
COPY ["svc2-blazorserver.csproj", "./"]
RUN dotnet restore "svc2-blazorserver.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "svc2-blazorserver.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "svc2-blazorserver.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "svc2-blazorserver.dll"]
