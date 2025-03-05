### **2-Tier Architecture (2-टियर आर्किटेक्चर)**

**2-Tier Architecture** ek client-server architecture hai jisme application ko do layers ya tiers mein divide kiya jata hai: ek **client layer (presentation layer)** aur ek **server layer (data layer)**. Is model mein, client directly server se data request karta hai, aur server data processing aur storage ka kaam karta hai.

### Components:
1. **Client Layer (Presentation Layer)**:
   - Yeh layer **frontend** ka kaam karti hai, jahan user application ke saath interact karta hai. Is layer mein user interface (UI) hota hai aur data ko present karne ka kaam hota hai.
   - Client server ko request bhejta hai aur response ko user ko dikhata hai.
   - Examples: Desktop applications, web browsers, ya mobile apps.

2. **Server Layer (Data Layer)**:
   - Server layer business logic aur data management handle karti hai. Server client se request receive karta hai, data process karta hai (jaise database query), aur result wapas bhejta hai.
   - Yeh layer database se data retrieve ya store karne ka kaam karti hai.
   - Examples: Database servers (SQL jaise MySQL, ya NoSQL jaise MongoDB), application servers.

### Kaise Kaam Karta Hai:
- **Client-side**: Jab user koi request karta hai (jaise query ya form submit karna), client server se data request karta hai.
- **Server-side**: Server woh request receive karta hai, data ko process karta hai (jaise database se fetch karna) aur result client ko bhejta hai.

### Example of 2-Tier Architecture:
1. **Client**: Ek user apne desktop application (jaise inventory management system) ko open karta hai.
2. **Server**: Application ek **database server** (jaise MySQL) ko request bhejta hai, jisme product details ya stock levels store hain. Server request ko process karta hai aur client ko data wapas bhejta hai.

### Advantages:
1. **Simplicity**: 2-Tier architecture ko implement karna relatively simple hota hai kyunki sirf do components (client aur server) hote hain.
2. **Fast Communication**: Jab intermediary layer nahi hota, toh data transfer comparatively fast hota hai.
3. **Direct Interaction**: Client aur server direct interact karte hain, jo system ko simple banata hai, khas kar small-scale applications ke liye.

### Disadvantages:
1. **Scalability Issues**: Jab number of clients badhta hai, server pe load increase hota hai, aur server bottleneck ban sakta hai. Is architecture mein scalability ki limitations hoti hain.
2. **Tight Coupling**: Client aur server ke beech direct dependency hoti hai. Agar ek layer mein koi change karna ho toh doosri layer ko bhi modify karna padta hai.
3. **Limited Flexibility**: Agar aapko business logic ya database ko modify karna ho, toh client ko bhi uske according update karna padta hai, jo flexibility ko limited bana deta hai.

### When to Use:
1. **Small to Medium Applications**: Jab application ko bahut jyada scale karne ki zarurat na ho aur limited users ho.
2. **Internal Applications**: Jaise koi application jo ek organization ke andar use hoti ho, jahan user local network (intranet) pe ho aur koi complex scalability na ho.
3. **Client-Server Database Applications**: Jaise ek stock management system jo direct client aur server ke beech interaction hota ho.

### Example Use Cases:
1. **Traditional Client-Server Applications**: Jaise ek accounting system jisme client application database server se directly interact karta hai.
2. **Database Client-Server Applications**: Ek simple inventory management system jo client application se data request karta hai aur server se data fetch karta hai.

### Summary:
**2-Tier Architecture** ek simple aur efficient model hai jahan client aur server ke beech direct communication hota hai. Yeh architecture small to medium applications ke liye suitable hai, lekin jab application ko scale karna ho, toh zyada complex architectures (jaise 3-Tier) ki zarurat padti hai.
