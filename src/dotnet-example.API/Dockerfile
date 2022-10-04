ARG DOTNET_VERSION

FROM mcr.microsoft.com/dotnet/aspnet:$DOTNET_VERSION AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:$DOTNET_VERSION AS build
WORKDIR /src
COPY /src/dotnet-example.API/. .

RUN dotnet restore "dotnet-example.API.csproj"
RUN dotnet build "dotnet-example.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet-example.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet-example.API.dll"]