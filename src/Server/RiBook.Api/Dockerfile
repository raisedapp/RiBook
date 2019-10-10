FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["RiBook.Api/RiBook.Api.csproj", "RiBook.Api/"]
RUN dotnet restore "RiBook.Api/RiBook.Api.csproj"
COPY . .
WORKDIR "/src/RiBook.Api"
RUN dotnet build "RiBook.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RiBook.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RiBook.Api.dll"]