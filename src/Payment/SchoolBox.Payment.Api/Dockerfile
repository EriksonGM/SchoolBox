#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/Payment/SchoolBox.Payment.Api/SchoolBox.Payment.Api.csproj", "src/Payment/SchoolBox.Payment.Api/"]
RUN dotnet restore "src/Payment/SchoolBox.Payment.Api/SchoolBox.Payment.Api.csproj"
COPY . .
WORKDIR "/src/src/Payment/SchoolBox.Payment.Api"
RUN dotnet build "SchoolBox.Payment.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SchoolBox.Payment.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SchoolBox.Payment.Api.dll"]