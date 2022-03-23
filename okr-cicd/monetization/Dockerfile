#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["monetization/monetization.csproj", "monetization/"]
RUN dotnet restore "monetization/monetization.csproj"
COPY . .
WORKDIR "/src/monetization"
RUN dotnet build "monetization.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "monetization.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "monetization.dll"]