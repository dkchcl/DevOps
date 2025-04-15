


### 1. **`docker pull mysql:8.0`**

Yeh command Docker Hub se MySQL ka version 8.0 ka image download kar rahi hai. Docker Hub ek public repository hai jahan se aap Docker images ko download kar sakte hain.

- **MySQL:8.0** ek official image hai jo MySQL ke version 8.0 ko represent karta hai. 
- Jab yeh image aapke local machine pe download ho jaata hai, tab aap ise container mein run kar sakte ho.

Is command ke run hone ke baad, aapke system mein MySQL ka image ready ho jaata hai.

### 2. **`docker run --name elearn_db -e MYSQL_ROOT_PASSWORD=Bbpl@#2304 -p 3306:3306 -d mysql:8.0`**

Yeh command ek Docker container run kar rahi hai jo MySQL database ko host karega. Let’s break it down:

- **`docker run`**: Yeh command ek container start karne ke liye use hota hai. Matlab, aap apne local machine pe ek instance (container) run kar rahe ho jo MySQL ko execute karega.
  
- **`--name elearn_db`**: Is flag se aap apne container ko ek naam de rahe hain. Yahan, container ka naam `elearn_db` hai. Yeh naam aapko baad mein use karne mein asaani hoti hai jab aapko container ke saath interact karna ho (e.g., `docker exec`, `docker stop` etc.).

- **`-e MYSQL_ROOT_PASSWORD=Bbpl@#2304`**: Yeh environment variable set kar raha hai jo MySQL root user ka password define karta hai. Is case mein root password `Bbpl@#2304` hai. Aap jab `mysql` client se connect karenge toh yeh password use karna padega.

- **`-p 3306:3306`**: Yeh port mapping ka kaam karta hai. Local machine ke port 3306 ko container ke port 3306 se connect karta hai. MySQL ka default port 3306 hota hai. Matlab, jab aap `localhost:3306` pe jaayenge, toh yeh request aapke MySQL container tak reach karegi.

- **`-d`**: Yeh flag container ko background mein run karne ke liye hai, taaki aap terminal ko free rakh sakein aur container apne kaam mein chalta rahe.

- **`mysql:8.0`**: Yeh aapke container ko batata hai ki kaunsa image use karna hai. Is case mein, yeh image `mysql:8.0` hai, jo ki MySQL version 8.0 ka official image hai.

### 3. **`docker exec -it elearn_db mysql -u root -p`**

Is command se aap apne `elearn_db` container ke andar jaakar MySQL shell ko access kar rahe hain:

- **`docker exec`**: Yeh command ek already running container ke andar kisi command ko execute karne ke liye use hoti hai. Yahan, aap container `elearn_db` ke andar command execute karne ja rahe hain.
  
- **`-it`**: Yeh two flags hain, `-i` (interactive) aur `-t` (allocate a pseudo-TTY). Iska matlab hai ki aapko container ke andar ek interactive session milta hai jisme aap commands execute kar sakte hain.

- **`elearn_db`**: Yeh aapke container ka naam hai, jise aapne pehle `--name` flag se diya tha.

- **`mysql -u root -p`**: Yeh command MySQL client ko run karti hai, jisme `-u root` ka matlab hai ki aap MySQL ke root user ke through login kar rahe hain, aur `-p` ka matlab hai ki aapko password enter karna hoga (jo aapne pehle set kiya tha: `Bbpl@#2304`).

Jab aap yeh command run karenge, aapko password enter karne ka prompt milega, aur agar password sahi hoga, toh aap MySQL shell ke andar enter kar jayenge.

### 4. **`CREATE DATABASE elearn_db;`**

Yeh SQL command ek naya database create karti hai jiska naam `elearn_db` hai. Aapko apne MySQL shell mein yeh command execute karni hoti hai taaki aapka new database ban sake.

- **`CREATE DATABASE`**: Yeh SQL command MySQL mein ek naya database banane ke liye use hoti hai.
- **`elearn_db`**: Yeh us database ka naam hai jo aap create karna chahte hain.

### 5. **`USE elearn_db;`**

Jab aap `CREATE DATABASE` execute karenge, tab `elearn_db` database create ho jayega, lekin usko use karne ke liye aapko `USE` command chalani padegi.

- **`USE`**: Yeh command batati hai MySQL ko ki aap kis database ke saath kaam karna chahte hain.
- **`elearn_db`**: Yeh database ka naam hai jise aap ab use karna chahte hain.

### 6. **Creating the `Courses` table:**

```sql
CREATE TABLE Courses (
    CourseId INT AUTO_INCREMENT PRIMARY KEY,
    CourseName VARCHAR(255) NOT NULL,
    InstructorName VARCHAR(255) NOT NULL,
    Lessons JSON NOT NULL
);
```

Yeh SQL query ek table banayegi jiska naam `Courses` hoga. Table mein 4 columns honge:

- **`CourseId`**: Yeh ek integer field hai jo automatically increment hoga jab naya record insert hoga. Yeh column primary key ke roop mein kaam karega, yani har course ka ek unique ID hoga.
- **`CourseName`**: Yeh field course ke naam ko store karegi. Yeh `VARCHAR` type hai, matlab string type, aur iska size 255 characters tak hoga. `NOT NULL` ka matlab hai ki yeh field empty nahi ho sakti.
- **`InstructorName`**: Yeh field course ke instructor ka naam store karegi. Iska bhi `VARCHAR(255)` type hai aur yeh bhi `NOT NULL` hai.
- **`Lessons`**: Yeh field course ke lessons ko store karegi, aur yeh field `JSON` type ki hogi. Aap ismein lessons ka structured data (like an array of lesson names or topics) store kar sakte hain.

### SHOW TABLES;
Yeh command aapko current database ke andar jitni bhi tables hain unka list de degi.
```
SHOW TABLES;
```
Yeh command elearn_db database ke andar jo bhi tables hain unka list dikhayegi. Agar aapne Courses table create kiya hai, toh woh bhi is list mein dikhega.

Output:
Example output kuch aise ho sakta hai:

```
+-------------------+
| Tables_in_elearn_db |
+-------------------+
| Courses            |
+-------------------+
1 row in set (0.00 sec)
```
Is output mein, Courses table dikh raha hai jo aapne create kiya tha.

### 7. **`docker inspect elearn_db`**

Yeh command aapko `elearn_db` container ki detailed information de deti hai. Isme aapko pata chalega:
- Container ka network configuration.
- Container ka mount points (kahan se kaunse files mount ki gayi hain).
- Environment variables.
- Container ka status (running hai ya stopped).

Is command se aapko ek JSON output milega jisme aapko sab information mil jayegi jo aapke container ke baare mein Docker ko pata hai.

---
