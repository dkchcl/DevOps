






```
from node:18
WORKDIR /dkc90
copy . .
run npm install
run npm run build
RUN apt update && apt install -y nginx
RUN cp -r build/* /var/www/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```




