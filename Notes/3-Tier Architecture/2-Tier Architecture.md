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


### **2-Tier Architecture Diagram (2-टियर आर्किटेक्चर डाइग्राम)**

**2-Tier Architecture** mein system ko do layers mein divide kiya jata hai: **Client Layer** aur **Server Layer**. **Client Layer** user interface ko handle karta hai aur directly **Server Layer** ke saath interact karta hai, jo business logic aur data storage ka kaam karta hai.

### **2-Tier Architecture Diagram:**

```
+---------------------------+            +-----------------------------+
|        Client Layer        |            |       Server Layer          |
|  (User Interface + Logic)  |  <----->   | (Business Logic + Data      |
|                           |            |        Storage)             |
+---------------------------+            +-----------------------------+
         (User)                                   (Database/Server)
```

### **डायग्राम का विवरण:**

1. **Client Layer (क्लाइंट लेयर)**:
   - **User Interface (UI)**: Yah wo layer hai jahan user application ke saath interact karta hai. Client layer presentation aur user input/output ko handle karta hai.
   - **Client Logic**: Client layer par kuch basic processing bhi ho sakti hai, lekin zyada tar data storage aur business logic ke liye server par depend karta hai.

2. **Server Layer (सर्वर लेयर)**:
   - **Business Logic**: Yah server pe data processing aur calculations ka kaam karta hai.
   - **Data Storage**: Server data ko store, retrieve aur update karta hai. Yah centralized database (jaise MySQL, PostgreSQL) ho sakta hai.

### **कैसे काम करता है:**
- **Client Layer** server ko request bhejta hai.
- **Server Layer** request ko process karta hai, business logic execute karta hai, aur data storage se data fetch ya update karta hai.
- Server apne results ko client ko bhejta hai, jahan user ko information dikhayi jaati hai.

### **2-Tier Architecture ka Example:**
- Ek **desktop application** (client) jo **database server** (server) ke saath directly interact karta hai, data fetch karne, update karne ya delete karne ke liye.
- Example: Ek **banking application** jahan client-side interface transactions ka data request karta hai, aur server-side business logic ko process karke database se data retrieve karta hai.

### **2-Tier Architecture ke Advantages (फायदे):**
1. **Simplicity**: Kam layers hone ki wajah se development simple aur fast hota hai.
2. **Better Performance**: Client aur server ke beech direct communication hone ki wajah se performance achi hoti hai.
3. **Centralized Data Management**: Data server mein centralized hota hai, jise manage aur maintain karna aasan hota hai.

### **Disadvantages (नुकसान):**
1. **Scalability Issues**: Jaise-jaise clients ka number badhta hai, server par load badh jata hai, jo performance ko affect kar sakta hai.
2. **Limited Flexibility**: Client aur server ke beech direct dependency hoti hai, jo ek layer mein changes karte waqt doosri layer ko bhi affect kar sakti hai.

### **Use Case (उदाहरण):**
- **Small to Medium Applications**: Jaise CRM (Customer Relationship Management) system ya inventory management systems.
