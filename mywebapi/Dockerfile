FROM microsoft/aspnetcore-build:2.0.7-2.1.105 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:2.0.7
WORKDIR /app
COPY --from=build-env /app/out .

# Expose port 9000
ENV ASPNETCORE_URLS http://+:9000
EXPOSE 9000

ENTRYPOINT ["dotnet", "mywebapi.dll"] 