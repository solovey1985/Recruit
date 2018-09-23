FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 3121
EXPOSE 3123

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Recruit/Recruit.csproj Recruit/
RUN dotnet restore Recruit/Recruit.csproj
COPY . .
WORKDIR /src/Recruit
RUN dotnet build Recruit.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Recruit.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Recruit.dll"]