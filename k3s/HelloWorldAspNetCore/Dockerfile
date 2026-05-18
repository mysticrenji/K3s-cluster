# Use Microsoft's official .NET image.
# https://hub.docker.com/r/microsoft/dotnet
FROM microsoft/dotnet:2.2-sdk AS build-env

# Install production dependencies.
# Copy csproj and restore as distinct layers.
WORKDIR /app
COPY *.csproj ./
RUN dotnet restore

# Copy local code to the container image.
COPY . ./

# Build a release artifact.
RUN dotnet publish -c Release -o out

# Make sure the app binds to port 8080
#ENV ASPNETCORE_URLS http://*:6000

# Run the web service on container startup.
#CMD ["dotnet", "out/HelloWorldAspNetCore.dll"]

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
ENV ASPNETCORE_URLS http://*:6000
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "HelloWorldAspNetCore.dll"]
