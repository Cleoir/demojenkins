FROM microsoft/aspnetcore-build:2.0 As build
WORKDIR /app
EXPOSE 90

COPY *.csproj ./
RUN dotnet restore

COPY . ./
RUN dotnet publish -c Release -o out

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM microsoft/aspnetcore:2.0 As runtime

WORKDIR /app

COPY --from=publish /app/out .

ENTRYPOINT ["dotnet", "WebApplication6.dll"]