When creating a **Virtual Network (VNet)** in **Microsoft Azure**, there are several fields and settings that you need to configure. Below is a comprehensive list and description of each field typically available during VNet creation in the Azure portal (as of 2024/2025):

---

## **1. Basics Tab**

### **Subscription**

* **Description**: The Azure subscription under which the VNet is created.
* **Purpose**: Determines billing and access.

### **Resource Group**

* **Description**: A container that holds related resources.
* **Purpose**: Organizes resources and allows collective management.

### **Name**

* **Description**: The name of the VNet.
* **Purpose**: Used to identify the network; must be unique within the resource group.

### **Region**

* **Description**: Azure region (e.g., East US, West Europe).
* **Purpose**: Specifies where the VNet is physically located.

---

## **2. IP Addresses Tab**

### **IPv4 Address Space**

* **Description**: CIDR block (e.g., 10.0.0.0/16) for the VNet.
* **Purpose**: Defines the range of IP addresses available for the network.

### **Add IPv4 address space**

* **Description**: Option to add additional CIDR blocks.
* **Purpose**: Allows flexibility for network growth or peering.

### **IPv6 Address Space (optional)**

* **Description**: CIDR block for IPv6 addresses.
* **Purpose**: Enables dual-stack configurations (IPv4 + IPv6).

### **Subnets**

* **Name**: Subnet name.
* **Subnet Address Range**: CIDR block (e.g., 10.0.0.0/24).
* **Purpose**: Divides the VNet into smaller address spaces for logical separation of workloads.

---

## **3. Security Tab**

### **BastionHost (Optional)**

* **Description**: Option to configure Azure Bastion.
* **Purpose**: Provides secure RDP/SSH without exposing public IPs.

### **DDoS Protection**

* **Options**: Basic (default), Standard (paid).
* **Purpose**: Protects against Distributed Denial of Service attacks.

### **Firewall (Optional)**

* **Description**: Option to create or associate an Azure Firewall.
* **Purpose**: Central control over network traffic using rules.

---

## **4. Tags Tab**

### **Name / Value pairs**

* **Description**: Metadata tags for organizing and tracking resources.
* **Purpose**: Helps with cost management, automation, and resource categorization.

---

## **5. Review + Create Tab**

* **Validation**

  * Azure checks all fields for completeness and correctness.
* **Create Button**

  * Finalizes and initiates deployment.

---

## **Other Considerations (Post-Creation)**

* **Network Security Groups (NSGs)**: Control inbound and outbound traffic to subnets or NICs.
* **Route Tables**: Custom routing for subnet traffic.
* **Peering**: Connects VNets across regions/subscriptions.
* **Service Endpoints / Private Endpoints**: Secure access to Azure services.

Would you like a sample configuration or a JSON/ARM template version of a VNet deployment?
