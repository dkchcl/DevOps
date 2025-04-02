

```
FROM node:18 AS build
WORKDIR /dkc90
COPY . .
RUN npm install
RUN npm run build
FROM nginx:alpine3.21
WORKDIR /usr/share/nginx/html
EXPOSE 80
COPY --from=build /dkc90/build* .
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# docker build -t dkc90:latest .
# docker run -d -p 80:80 dkc90:latest
```
