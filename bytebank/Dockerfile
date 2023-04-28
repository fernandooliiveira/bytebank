FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["bytebank/bytebank.csproj", "bytebank/"]
RUN dotnet restore "bytebank/bytebank.csproj"
COPY . .
WORKDIR "/src/bytebank"
RUN dotnet build "bytebank.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "bytebank.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "bytebank.dll"]
