## **Azure Virtual Network (VNet)** 

---

### 🔵 Azure Virtual Network (VNet) Kya Hai?

Soch le tu ek **building bana raha hai cloud me**, jisme tu apne servers, computers, aur applications ko rakhna chahta hai. Ab tujhe chahiye ki ye sab ek **private network** me ho jahan koi outsider bina permission ke ghus na sake.

Toh Microsoft Azure tujhko ye facility deta hai jiska naam hai **Virtual Network (VNet)**.

---

### 🔧 Iska kaam kya hota hai?

VNet ek **private network hota hai Azure ke andar**, jisme tu:

* Apne **virtual machines (VMs)** ko connect kar sakta hai
* **Internet access control** kar sakta hai (kaun bahar ja sakta hai, kaun andar aa sakta hai)
* Alag-alag Azure services ko securely connect kar sakta hai
* Apne **on-premises network** (jo tere office me hai) ko Azure se jod sakta hai VPN ke through

---

### 🧱 Main Components of VNet:

1. **Subnets:**

   * Tere VNet ke andar tu alag-alag zones bana sakta hai jaise:

     * ek subnet web servers ke liye
     * ek subnet database ke liye
     * ek subnet application ke liye

2. **IP Addressing:**

   * Tu decide karta hai kaunse IP address use honge is network me (jaise gharon ke address hote hain)

3. **Network Security Groups (NSG):**

   * Tu rules bana sakta hai ki kaun kis subnet ya VM se baat kar sakta hai (jaise gatekeeper)

4. **Route Tables:**

   * Ye decide karta hai traffic kis raste se jayega (road map jaisa)

5. **VPN Gateway / ExpressRoute:**

   * Agar tu apne office ke network ko Azure ke VNet se jodna chahta hai securely, toh ye use hota hai

---

### 📦 Example:

Maan le:

* Tu ek e-commerce website bana raha hai
* Tu chahata hai:

  * Web servers public ho (users access kar sake)
  * Database servers private ho (sirf web server access kare)
* Tu ek VNet banata hai:

  * Subnet1 – Web (Public IP allowed)
  * Subnet2 – Database (No public access)
* Dono subnets secure tareeke se ek dusre se baat karte hain, but bahar se koi database tak nahi pahunch sakta

---

### 🔐 Security?

Azure VNet secure hota hai:

* **By default, isolated hota hai**
* NSG aur firewalls se tu full control le sakta hai
* Tu monitoring bhi kar sakta hai (jaise ki traffic logs)

---

### 🤔 Kyon Zaroori Hai?

* Secure communication chahiye
* Alag-alag components ko logically organize karna hai
* Scalability aur control chahiye network pe

---
