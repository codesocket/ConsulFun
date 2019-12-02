FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["ConsulFun/ConsulFun.csproj", "ConsulFun/"]
RUN dotnet restore "ConsulFun/ConsulFun.csproj"
COPY . .
WORKDIR "/src/ConsulFun"
RUN dotnet build "ConsulFun.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsulFun.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsulFun.dll"]