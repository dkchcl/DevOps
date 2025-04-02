## Elearn_fronend Docker file:

```dockerfile
# Use Node.js version 18 as the base image
FROM node:18

# Set the working directory inside the container to /dkc90
WORKDIR /dkc90

# Copy all files from the current directory on your machine to the working directory in the container
COPY . .

# Install all the dependencies defined in package.json
RUN npm install

# Build the application (usually creates a 'build' folder)
RUN npm run build

# Update package list and install nginx (web server)
RUN apt update && apt install -y nginx

# Copy the built app from the 'build' folder to the Nginx serving directory
RUN cp -r build/* /var/www/html

# Expose port 80 for HTTP traffic
EXPOSE 80

# Start Nginx in the foreground to serve the app
CMD ["nginx", "-g", "daemon off;"]                    # or mention ENTRYPOINT ["nginx", "-g", "daemon off;"] 
```

### Comment Breakdown:

### 1. `FROM node:18`
- **Kya ho raha hai?**: Yeh line base image specify karti hai. Matlab hum ek aise Docker image use kar rahe hain jo Node.js 18 already install kiya hua hai. Matlab Node.js ko install karne ka kaam humne pehle hi kar diya.

### 2. `WORKDIR /dkc90`
- **Kya ho raha hai?**: Yeh command ek folder banata hai container ke andar jiska naam `/dkc90` hai. Ab se hum saari commands is folder ke andar run karenge.

### 3. `COPY . .`
- **Kya ho raha hai?**: Yeh line tumhare local system se sab kuch (`.` ka matlab hai current folder) Docker container ke andar copy kar rahi hai. Matlab jo files tumhare machine mein hain, woh container ke andar bhi aa jayengi.

### 4. `RUN npm install`
- **Kya ho raha hai?**: `npm install` ka matlab hai, Node.js ki jo dependencies tumne `package.json` mein likhi hain, unko install karo. Matlab, jo packages tumhare app ko chalane ke liye chahiye, woh install ho jayenge.

### 5. `RUN npm run build`
- **Kya ho raha hai?**: Jab tumne apna app bana liya, toh ab usko production ke liye ready karna padta hai. `npm run build` se tumhara app build ho jata hai (yani optimized, minified version ban jata hai jo production mein chalta hai).

### 6. `RUN apt update && apt install -y nginx`
- **Kya ho raha hai?**: Yeh line container mein Nginx web server install kar rahi hai. Nginx ka kaam hai tumhare app ko serve karna (basically, yeh HTTP requests ko handle karta hai). `apt update` se system ka package list update hota hai, aur `apt install -y nginx` se Nginx install hota hai.

### 7. `RUN cp -r build/* /var/www/html`
- **Kya ho raha hai?**: Tumhare app ka jo `build` folder bana hai, uske andar saari files ko Nginx ke default folder (`/var/www/html`) mein copy kar diya gaya hai. Yeh Nginx ko batata hai ki kaun si files serve karni hain jab koi user website open karega.

### 8. `EXPOSE 80`
- **Kya ho raha hai?**: Yeh line container ko port 80 pe expose kar rahi hai. Port 80 ka matlab hai HTTP traffic. Jab container run hoga, toh Nginx iss port pe tumhare app ko serve karega.

### 9. `CMD ["nginx", "-g", "daemon off;"]`
- **Kya ho raha hai?**: Jab container start hoga, yeh command Nginx ko run karegi. `-g "daemon off;"` ka matlab hai ki Nginx ko background mein run nahi hone dena hai, balki foreground mein run karna hai, taaki container chal raha rahe.

---

### Simple Explanation:
Is Dockerfile mein:
- Hum apne Node.js app ko container mein setup kar rahe hain.
- Build kar rahe hain.
- Uske baad Nginx web server ko install karke, usko container mein serve karne ke liye set kar rahe hain.
- Aur, finally, port 80 pe Nginx ko run karwa rahe hain taaki tumhara app publicly accessible ho jaye.





