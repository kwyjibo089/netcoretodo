FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 18757
EXPOSE 44310

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AspNetCoreTodo.csproj", ""]
RUN dotnet restore "AspNetCoreTodo.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "AspNetCoreTodo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AspNetCoreTodo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNetCoreTodo.dll"]