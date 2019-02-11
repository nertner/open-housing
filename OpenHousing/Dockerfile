FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["OpenHousing/OpenHousing.csproj", "OpenHousing/"]
RUN dotnet restore "OpenHousing/OpenHousing.csproj"
COPY . .
WORKDIR "/src/OpenHousing"
RUN dotnet build "OpenHousing.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "OpenHousing.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "OpenHousing.dll"]