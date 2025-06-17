## **Azure Subnet** 

---

## 🔷 Azure Subnet – Simple Bhasha Mein

### 🔹 Pehle Basic Samajh:

* **Azure** ek cloud platform hai jaha tu apne servers, databases, applications wagairah chala sakta hai bina physical hardware ke.
* **Virtual Network (VNet)** ek tarah ka *digital area* hai jaha tu apne Azure resources (jaise VM, databases, etc.) ko secure tarike se connect karta hai.

---

## 🧱 Subnet Kya Hai?

**Subnet** ka matlab hai **Sub-Network**. Ye ek **Virtual Network ke andar ka chhota hissa** hota hai.

Soch:

> Jaise ek city (Virtual Network) hai, uske andar kai mohalla (Subnets) hote hain.

---

### 🔍 Kyun Banate Hain Subnet?

1. **Resources ko organize karne ke liye**

   * Web server ek subnet mein, database dusre mein
2. **Security control ke liye**

   * Har subnet ke upar alag rules (NSG - Network Security Groups) laga sakte hain
3. **Traffic control ke liye**

   * Kis subnet se bahar ja sakta hai, kis se nahi – ye define kar sakte hain

---

## 🧠 Ek Chhota Example:

### 🏙 Virtual Network:

* Name: `MyVNet`
* Address space: `10.0.0.0/16`

### 🧩 Subnets:

1. `WebSubnet` – `10.0.1.0/24`
2. `AppSubnet` – `10.0.2.0/24`
3. `DBSubnet` – `10.0.3.0/24`

Iska matlab:

* Tu apna Web Server `WebSubnet` mein rakhega
* Application Server `AppSubnet` mein
* Database `DBSubnet` mein

Har subnet ke beech communication tu allow ya restrict kar sakta hai, jaise firewall ki tarah.

---

## 🔐 Subnet ke Saath Kya Kya Ho Sakta Hai?

| Feature                  | Kya Karta Hai                                                               |
| ------------------------ | --------------------------------------------------------------------------- |
| **NSG (Security Group)** | Subnet ke andar traffic allow/deny karta hai                                |
| **Route Table**          | Traffic kis direction mein jaye – ye define karta hai                       |
| **Peering**              | Do VNets ko connect karta hai                                               |
| **VPN Gateway**          | On-premises (tera ghar ka data center) se Azure subnet ko connect karta hai |

---

## 💡 Ek Real Life Analogy:

> 🏙 VNet = Ek society
>
> 🏠 Subnet = Society ke alag-alag blocks
>
> 🚧 NSG = Security guard jo decide karta hai kaun andar ja sakta hai
>
> 📞 VPN = Phone line jo tu ghar se society ko connect karta hai

---

