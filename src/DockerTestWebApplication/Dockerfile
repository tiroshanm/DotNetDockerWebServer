FROM microsoft/aspnetcore-build:1.0.1 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY . ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

RUN ls bin/Release/netcoreapp1.0

# Build runtime image
FROM microsoft/aspnetcore:1.0.1
WORKDIR /app
EXPOSE 5000
COPY --from=build-env /app/out .
COPY --from=build-env /app/bin/Release/netcoreapp1.0/app.dll .
RUN ls
ENTRYPOINT ["dotnet", "app.dll"]
