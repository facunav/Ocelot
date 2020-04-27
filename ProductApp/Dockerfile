FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["ProductApp/ProductApp.csproj", "ProductApp/"]
RUN dotnet restore "ProductApp/ProductApp.csproj"
COPY . .
WORKDIR "/src/ProductApp"
RUN dotnet build "ProductApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ProductApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ProductApp.dll"]