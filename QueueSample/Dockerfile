FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["QueueSample/QueueSample.csproj", "QueueSample/"]
RUN dotnet restore "QueueSample/QueueSample.csproj"
COPY . .
WORKDIR "/src/QueueSample"
RUN dotnet build "QueueSample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "QueueSample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "QueueSample.dll"]
