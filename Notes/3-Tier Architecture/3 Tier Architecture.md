### **3-Tier Architecture (3-टियर आर्किटेक्चर)**

**3-Tier Architecture** ek software architecture hai jisme application ko teen alag layers mein divide kiya jata hai: **Presentation Layer**, **Business Logic Layer**, aur **Data Layer**.

### Components:
1. **Presentation Layer**: User interface (UI), jahan user interact karta hai.
2. **Business Logic Layer**: Application logic, jo data ko process karta hai.
3. **Data Layer**: Database, jahan data store aur retrieve hota hai.

### Kaise Kaam Karta Hai:
1. **Presentation Layer** se user request aati hai.
2. **Business Logic Layer** request ko process karta hai.
3. **Data Layer** se data fetch karke presentation layer ko bheja jata hai.

### Advantages:
1. **Modularity**: Har layer apne kaam ko handle karti hai, jo maintenance aur scaling ko asaan banata hai.
2. **Scalability**: Layers ko independently scale kiya ja sakta hai.
3. **Security**: Sensitive data ko alag layer mein rakha jata hai.

### Disadvantages:
1. **Complexity**: Zyada layers hone se system complex ho sakta hai.
2. **Performance Overhead**: Layers ke beech communication se performance thoda slow ho sakta hai.

### Use Cases:
- **Large Applications**: Jaise e-commerce websites, banking systems.
- **Enterprise Applications**: Jaise ERP, CRM systems.

### Summary:
**3-Tier Architecture** large-scale applications ke liye best hai, jahan modularity, scalability, aur security ki zaroorat hoti hai.
