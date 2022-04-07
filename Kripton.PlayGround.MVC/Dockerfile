FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Kripton.PlayGround.MVC/Kripton.PlayGround.MVC.csproj", "Kripton.PlayGround.MVC/"]
RUN dotnet restore "Kripton.PlayGround.MVC/Kripton.PlayGround.MVC.csproj"
COPY . .
WORKDIR "/src/Kripton.PlayGround.MVC"
RUN dotnet build "Kripton.PlayGround.MVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Kripton.PlayGround.MVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Kripton.PlayGround.MVC.dll"]
