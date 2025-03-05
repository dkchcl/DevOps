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
