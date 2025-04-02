
```
# Use the official .NET SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:8.0

# Set the working directory inside the container
WORKDIR /dkc23

# Copy the application code into the container
COPY . .

# Restore the .NET project dependencies
RUN dotnet restore

# Build the .NET project in Release configuration
RUN dotnet build --configuration Release

# Publish the .NET project for production
RUN dotnet publish -c Release -o ./publish

# Set the entry point for the application (run the published application)
ENTRYPOINT ["dotnet", "publish/ElearnBackend.dll"]
```

#### Make Docker Image:
```
docker build -t elearn-backend:v1 .
```
#### Run container:
```
docker run -p 5000:5000 -p 5001:5001 elearn-backend
```
**Hit on local computer with Swagger:**
```
localhost:port/swagger
```





