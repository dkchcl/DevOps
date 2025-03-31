### Frontend Steps:

Here's how you can do it:

```dockerfile
# Use Node.js base image
FROM node:18

# Set the working directory inside the container
WORKDIR /dkc90

# Copy the contents of the current directory (.) to the container’s /dkc90 directory
COPY . .

# Install dependencies for the Node.js application
RUN npm install

# Build the application (e.g., a React app or similar)
RUN npm run build

# Install Nginx in the container
RUN apt update && apt install -y nginx

# Copy the build output to Nginx's default folder
RUN cp -r build/* /var/www/html

# Expose port 80 to allow external access to the container
EXPOSE 80

# Set the entrypoint to start Nginx when the container runs
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

### Explanation:
1. **FROM node:18**: The base image is Node.js 18.
2. **WORKDIR /dkc90**: The working directory is set to `/dkc90` inside the container.
3. **COPY . .**: Copies all files from the current directory (where the Dockerfile is located) into the container’s `/dkc90` directory.
4. **RUN npm install**: Installs all dependencies required by the application.
5. **RUN npm run build**: Builds the project (e.g., compiles assets, etc.).
6. **RUN apt update && apt install -y nginx**: Installs Nginx, which will serve the built static files.
7. **RUN cp -r build/* /var/www/html**: Copies the build output from the project’s `build` directory to Nginx’s default web directory.
8. **EXPOSE 80**: Exposes port 80 for web traffic.
9. **ENTRYPOINT ["nginx", "-g", "daemon off;"]**: The `ENTRYPOINT` command runs Nginx in the foreground when the container starts. The `-g "daemon off;"` option is used to prevent Nginx from running as a background process, ensuring the container stays alive.

### Notes:
- The `ENTRYPOINT` ensures that when the container starts, Nginx serves the static content from the `/var/www/html` directory.
- If you need to pass additional configuration or change settings for Nginx, you can modify the `nginx.conf` file and copy it to `/etc/nginx/nginx.conf` using another `COPY` command before the `ENTRYPOINT` step.

This setup should make the container serve the static assets of your Node.js project using Nginx on port 80.


