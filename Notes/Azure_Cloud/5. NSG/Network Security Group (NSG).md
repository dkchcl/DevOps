Creating a **Network Security Group (NSG)** in **Microsoft Azure** involves configuring several fields and settings to control inbound and outbound network traffic to Azure resources. Here's a detailed breakdown of all the fields typically involved in NSG creation and rule configuration, whether you're using the Azure Portal, CLI, PowerShell, or ARM templates.

---

## 🧩 **Basic NSG Configuration Fields**

These are the fields you fill out when **creating an NSG** (before adding rules):

### 1. **Subscription**

* **Description**: The Azure subscription under which the NSG will be created.
* **Example**: `Pay-As-You-Go`

### 2. **Resource Group**

* **Description**: Logical container for the NSG.
* **Purpose**: Helps organize and manage related Azure resources.
* **Example**: `myResourceGroup`

### 3. **Name**

* **Description**: The name of the NSG.
* **Constraints**: Must be unique within the resource group.
* **Example**: `myNSG`

### 4. **Region (Location)**

* **Description**: The Azure region where the NSG will be created.
* **Purpose**: Must match the region of the virtual network (VNet) or subnet where NSG is applied.
* **Example**: `East US`, `West Europe`

---

## 🚦 **Security Rules Fields (Inbound/Outbound Rules)**

Each NSG can have **inbound** and **outbound security rules** that control traffic. Each rule includes:

### 1. **Name**

* **Description**: Unique identifier for the rule within the NSG.
* **Example**: `AllowHTTPInbound`

### 2. **Priority**

* **Description**: Determines the order in which rules are applied (lower number = higher priority).
* **Range**: `100` to `4096`
* **Example**: `100`

### 3. **Direction**

* **Values**:

  * `Inbound` – for traffic coming **into** a resource.
  * `Outbound` – for traffic going **out of** a resource.

### 4. **Source**

* **Options**:

  * `Any`
  * `IP Addresses` (CIDR format)
  * `Service Tag` (e.g., `Internet`, `VirtualNetwork`, `AzureLoadBalancer`)
  * `Application Security Group` (if configured)

### 5. **Source Port Ranges**

* **Description**: Port(s) traffic originates from.
* **Example**: `*` (any), `80`, `1024-65535`

### 6. **Destination**

* **Same options as Source**

  * `Any`
  * `IP Addresses`
  * `Service Tag`
  * `Application Security Group`

### 7. **Destination Port Ranges**

* **Description**: Target ports.
* **Example**: `22`, `443`, `80`, `3389`, `*`

### 8. **Protocol**

* **Options**:

  * `Any`
  * `TCP`
  * `UDP`
  * `ICMP`

### 9. **Action**

* **Options**:

  * `Allow`
  * `Deny`
* **Description**: Whether to permit or block the matched traffic.

### 10. **Description (Optional)**

* **Description**: Human-readable explanation of the rule’s purpose.
* **Example**: `Allow HTTP traffic to web servers`

---

## 🧰 **Optional NSG Features**

### 1. **Application Security Groups (ASGs)**

* **Purpose**: Allow grouping of VMs by name and applying NSG rules to the group.
* **Benefit**: Better manageability over managing IP addresses.

### 2. **Service Tags**

* **Purpose**: Simplify NSG rule definition by using predefined tags.
* **Common Tags**:

  * `Internet`
  * `VirtualNetwork`
  * `AzureLoadBalancer`
  * `Storage`
  * `AppGatewayBackend`

---

## 🔗 **NSG Association Targets**

After creating an NSG, you must **associate it** with:

### 1. **Subnets**

* Applies rules to all network interfaces in the subnet.

### 2. **Network Interfaces (NICs)**

* Applies rules only to the attached VM’s NIC.

> 🔒 **Important:** NSG rules are **stateful** — meaning return traffic for allowed inbound flows is automatically permitted.

---

## ✅ Best Practices

* Always use **specific IP ranges and ports** where possible.
* Use **ASGs** or **service tags** instead of IP addresses.
* Place **deny rules** with lower priorities to block specific traffic.
* Regularly **review NSG rules** for security compliance.

---

Would you like an example NSG setup using Azure CLI or an ARM template?

