##FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
#WORKDIR /src
#COPY ["CartService/CartService.csproj", "CartService/"]
#RUN dotnet restore "CartService/CartService.csproj"
#COPY . .
#WORKDIR "/src/CartService"
#RUN dotnet build "CartService.csproj" -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "CartService.csproj" -c Release -o /app/publish
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "CartService.dll"]

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 as build-env
WORKDIR /app

COPY *.csproj ./
RUN dotnet restore 

COPY . ./

RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:3.0
WORKDIR /app
EXPOSE 80
COPY --from=build-env /app/out .
ENTRYPOINT [ "dotnet", "CartService.dll"]