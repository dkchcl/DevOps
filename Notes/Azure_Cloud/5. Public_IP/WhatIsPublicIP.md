## **Azure Public IP**--

---

### 🔹 **What is an Azure Public IP?**

A **Public IP Address** in Azure is an IP address that is **accessible from the internet**. It allows external devices (like your personal computer or users across the world) to connect to Azure resources.

If you set up something like a **Virtual Machine (VM)** in Azure and want to access it over the internet, you’ll need to assign a **Public IP** to it.

---

### 🔹 Simple Example:

Imagine you create a **Virtual Machine (VM)** in Azure and you want to connect to it using **Remote Desktop (RDP)** from your home.

You can’t do that unless your VM has a **Public IP Address**, which acts like the "door number" through which the internet finds and connects to your VM.

---

### 🔹 Key Features of Azure Public IP:

| Feature                 | Description                                                                   |
| ----------------------- | ----------------------------------------------------------------------------- |
| **Internet Accessible** | Connects your Azure resource directly to the internet                         |
| **Static or Dynamic**   | Can be fixed (static) or changeable (dynamic)                                 |
| **IPv4 or IPv6**        | Supports both IP versions (IPv4 is most common)                               |
| **SKU Types**           | Two types – **Basic** and **Standard** (Standard is more secure and scalable) |

---

### 🔹 Where is Public IP used in Azure?

1. **Virtual Machines (VMs)** – For remote access (SSH, RDP)
2. **Load Balancers** – For distributing web traffic
3. **Application Gateways** – For hosting web apps securely
4. **VPN Gateways / Firewalls** – For secure internet connections
5. **NAT Gateways** – For outbound internet connections

---

### 🔹 How to Create a Public IP in Azure?

1. Go to **Azure Portal**
2. Click on **Create a Resource**
3. Search for **Public IP Address**
4. Fill in:

   * Name
   * Resource Group
   * Region
   * Type (Static or Dynamic)
   * SKU (Basic or Standard)
5. Click **Create**

---

### 🔹 Static vs Dynamic Public IP

| Type        | Meaning                  | When to Use                                           |
| ----------- | ------------------------ | ----------------------------------------------------- |
| **Static**  | The IP never changes     | When you need a permanent IP (e.g., for DNS settings) |
| **Dynamic** | IP may change on restart | When a fixed IP is not important                      |

---



