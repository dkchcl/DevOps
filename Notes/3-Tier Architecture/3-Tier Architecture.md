### **3-Tier Architecture (3-टियर आर्किटेक्चर)**

**3-Tier Architecture** ek software architecture pattern hai jo application ko teen distinct layers mein divide karta hai: **Presentation Layer**, **Business Logic Layer**, aur **Data Layer**. Yeh architecture large-scale applications mein use hota hai, jahan ek layer ka kaam doosre layer se alag hota hai. Isse modularity, maintainability, aur scalability improve hoti hai.

### Components:

1. **Presentation Layer (User Interface Layer)**:
   - Yeh layer **frontend** ko represent karti hai, jahan user application ke saath interact karta hai. Presentation layer ka kaam user ko data dikhana aur user input lena hai.
   - Is layer mein user interface hota hai, jahan user form submit karta hai ya data dekhne ke liye queries karta hai.
   - Example: Web browser, mobile apps, or desktop applications.

2. **Business Logic Layer (Application Layer)**:
   - Yeh layer **backend logic** ko handle karti hai. Business logic layer wo processing karta hai jo user ki request ke saath related hota hai. Yeh layer application ka core logic hota hai aur business rules ko implement karta hai.
   - Yeh layer presentation layer se aane wale data ko process karti hai, aur data ko data layer (database) se fetch ya update karne ke liye request bhejti hai.
   - Example: Web servers, application servers (Apache Tomcat, WebLogic).

3. **Data Layer (Database Layer)**:
   - Yeh layer data ko store karti hai aur manage karti hai. Isme database ya file system hota hai jahan data store hota hai. Yeh layer data ko store, retrieve, aur modify karti hai.
   - Business logic layer is layer ke saath interact karta hai jab usse data ki zaroorat hoti hai.
   - Example: Database systems like MySQL, PostgreSQL, MongoDB.

### Kaise Kaam Karta Hai:
1. **Presentation Layer**: User koi request karta hai, jaise ek form submit karna ya search karna.
2. **Business Logic Layer**: Presentation layer ki request ko receive karta hai, aur us request ko process karta hai (e.g., user authentication, calculation).
3. **Data Layer**: Agar business logic layer ko data ki zaroorat hoti hai, toh wo data layer se request karta hai (e.g., database query) aur result receive karta hai.
4. **Return Flow**: Data jo data layer se aata hai, wo business logic layer ke through presentation layer ko bheja jata hai, jahan user ko dikhaya jata hai.

### Example of 3-Tier Architecture:
1. **Presentation Layer**: Ek user web browser ya mobile app ke through e-commerce website pe search karta hai.
2. **Business Logic Layer**: Server user ki search request ko process karta hai, jaise product categories ya price range ke hisaab se results dikhana.
3. **Data Layer**: Server data layer (e.g., MySQL database) se product data fetch karta hai aur presentation layer ko bhejta hai.

### Advantages:
1. **Modularity**: Har layer apne responsibilities ko handle karti hai, jo application ko modular banata hai. Agar ek layer mein change karna ho, toh doosri layers par koi impact nahi hota.
2. **Scalability**: Agar ek layer ko zyada load mil raha ho, toh us layer ko independently scale kiya ja sakta hai (e.g., business logic layer ko zyada server resources diye ja sakte hain).
3. **Maintainability**: Har layer ki separate functionality hoti hai, jo system ko maintain karne mein asaan bana deti hai. Agar kisi layer ko upgrade ya modify karna ho, toh baaki layers unaffected rehti hain.
4. **Security**: Data access ko restrict karne ke liye, layers ko separate kiya jata hai. Sensitive data ko data layer mein rakha jata hai, jo business logic aur presentation layer se isolated hota hai.

### Disadvantages:
1. **Complexity**: 3-Tier architecture thoda complex ho sakta hai, especially jab application ko manage aur scale karna ho.
2. **Performance Overhead**: Layers ke beech data transfer hota hai, jo performance ko thoda slow kar sakta hai, khaas kar jab data ka size bada ho.
3. **Cost**: Multiple layers ke liye additional hardware resources ki zaroorat ho sakti hai, jo overall cost ko badha sakta hai.

### When to Use:
1. **Large-Scale Applications**: Jab application ko scale karne ki zaroorat ho aur users ke liye complex functionalities provide karni ho.
2. **Web Applications**: Jaise e-commerce websites, banking systems, content management systems (CMS).
3. **Enterprise Applications**: Jab multiple users aur heavy data processing ki requirement ho, jaise ERP (Enterprise Resource Planning) systems, CRM (Customer Relationship Management) systems.

### Example Use Cases:
1. **E-commerce Websites**: User product search karne ke liye presentation layer (web browser) use karta hai, business logic layer server-side processing karta hai, aur data layer se product information fetch ki jati hai.
2. **Online Banking Systems**: User bank account details check karta hai (presentation layer), server transactions process karta hai (business logic layer), aur database se account data retrieve karta hai (data layer).

### Summary:
**3-Tier Architecture** ek efficient aur scalable solution hai, jo large applications mein use hota hai. Har layer ko alag responsibilities di jati hain, jo system ko modular, maintainable, aur secure banata hai. Is architecture ka use tab hota hai jab application ko complex functionality, scalability, aur flexibility ki zaroorat ho.




### **3-Tier Architecture Diagram (3-टियर आर्किटेक्चर डाइग्राम)**

**3-Tier Architecture** mein system ko teen layers mein divide kiya jata hai: **Presentation Layer**, **Business Logic Layer**, aur **Data Layer**. Har layer ka apna specific kaam hota hai aur yeh layers ek doosre se interact karti hain.

### **3-Tier Architecture Diagram:**

```
+---------------------------+          +-----------------------------+          +---------------------------+
|     Presentation Layer     |  <-----> |   Business Logic Layer      |  <-----> |       Data Layer          |
|     (User Interface)       |          |     (Application Logic)     |          |    (Database Storage)     |
+---------------------------+          +-----------------------------+          +---------------------------+
        (User)                           (Business Processing)                   (Data Management)
```

### **डायग्राम का विवरण:**

1. **Presentation Layer (प्रेजेंटेशन लेयर)**:
   - **User Interface (UI)**: Yah wo layer hai jahan user application ke saath interact karta hai. User ko data dikhana aur user se input lena is layer ka kaam hai.
   - Yeh layer sirf data ko present karti hai aur user ke inputs ko business logic layer ko bhejti hai.

2. **Business Logic Layer (बिजनेस लॉजिक लेयर)**:
   - Yah layer application ka core logic handle karti hai, jaise calculations, validations, aur business rules. Is layer ka kaam data ko process karna aur request ke hisaab se decision lena hai.
   - Jab client presentation layer se request bhejta hai, toh yeh layer wo request process karti hai aur data layer se data fetch ya update karti hai.

3. **Data Layer (डेटा लेयर)**:
   - Yah layer data ko store karti hai aur retrieve karti hai. Yeh layer server par hoti hai aur database (jaise MySQL, PostgreSQL) ka use karti hai.
   - Business logic layer data layer se data retrieve karne ya store karne ke liye interact karti hai.

### **कैसे काम करता है:**
- **Presentation Layer** se user koi request bhejta hai, jaise kisi product ko search karna.
- **Business Logic Layer** wo request process karta hai, jaise query ko validate karna aur data ko process karna.
- **Data Layer** se business logic layer data retrieve karta hai ya update karta hai.
- Server ka result **Business Logic Layer** ko return hota hai, jo fir **Presentation Layer** ko data bhejta hai aur user ko display karta hai.

### **Example of 3-Tier Architecture:**
- **E-commerce Website**: 
  1. **Presentation Layer**: User website par visit karta hai, products search karta hai.
  2. **Business Logic Layer**: Server product search query ko process karta hai, filter apply karta hai.
  3. **Data Layer**: Server database se products retrieve karta hai aur return karta hai.

### **Advantages (फायदे):**
1. **Modularity**: Har layer apne specific kaam ko handle karti hai, jo system ko modular banaata hai.
2. **Scalability**: Agar system ko scale karna ho, toh har layer ko independently scale kiya ja sakta hai.
3. **Maintainability**: Har layer ko alag rakha jata hai, jisse maintenance aur upgrades aasan hote hain.
4. **Security**: Data access ko restricted rakha jata hai, jisse system ko zyada secure banaya ja sakta hai.

### **Disadvantages (नुकसान):**
1. **Complexity**: Teen layers hone ke wajah se system thoda complex ho sakta hai.
2. **Performance Overhead**: Data transfer aur communication ke liye layers ke beech interaction hota hai, jo performance ko thoda slow kar sakta hai.

### **Use Cases (उदाहरण):**
- **Large-Scale Web Applications**: Jaise online banking systems, e-commerce websites, content management systems (CMS).
- **Enterprise Applications**: Jaise ERP (Enterprise Resource Planning) systems.
