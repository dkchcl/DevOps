### Elearn_frontend Dockerfile with lightweight image:


Here is your Dockerfile with clear and concise comments explaining each step:

```dockerfile
# Stage 1: Build the application using Node.js 18
FROM node:18 AS build

# Set the working directory inside the container to /dkc90
WORKDIR /dkc90

# Copy all files from the local machine to the container's working directory
COPY . .

# Install all Node.js dependencies from package.json
RUN npm install

# Build the application (usually creates a 'build' directory)
RUN npm run build

# Stage 2: Set up Nginx to serve the built application
FROM nginx:alpine3.21

# Set the working directory inside the Nginx container
WORKDIR /usr/share/nginx/html

# Copy the built app from the first stage (Node.js build) to the Nginx serving directory
COPY --from=build /dkc90/build* .

# Expose port 80 so the app can be accessed via HTTP
EXPOSE 80

# Start Nginx in the foreground to serve the app
CMD ["nginx", "-g", "daemon off;"]                        # or use- ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

### Comment Breakdown:
- **Stage 1: Build**:
  - **FROM node:18**: Uses Node.js 18 to build the app.
  - **WORKDIR /dkc90**: Sets the directory where app files will be placed and where the build will happen.
  - **COPY . .**: Copies local files to the container.
  - **RUN npm install**: Installs dependencies from `package.json`.
  - **RUN npm run build**: Builds the app for production (creates a `build/` folder).

- **Stage 2: Nginx Setup**:
  - **FROM nginx:alpine3.21**: Uses a lightweight Nginx image to serve the app.
  - **WORKDIR /usr/share/nginx/html**: Default directory where Nginx looks for web files.
  - **COPY --from=build**: Copies the built app from the previous stage (Node.js build) into Nginx's web directory.
  - **EXPOSE 80**: Exposes port 80 to serve the app over HTTP.
  - **CMD**: Runs Nginx to serve the app in the foreground.
  - **ENTRYPOINT** `["nginx", "-g", "daemon off;"]:` Runs Nginx in the foreground (the `"-g", "daemon off;"` option keeps Nginx running in the foreground, preventing the container from stopping immediately).

### Build and Run Instructions:
- **Build Image**: `docker build -t elearn_frontend:latest .`
- **Run Container**: `docker run -d -p 85:80 elearn_frontend:latest`

