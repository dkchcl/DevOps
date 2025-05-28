
When creating a **subnet** in a **Virtual Network (VNet)** in **Microsoft Azure**, there are several fields and configurations to understand. Each plays a role in defining the subnet’s properties, security, routing, and connectivity. Here's a detailed breakdown of each field available during subnet creation in the Azure portal or via tools like Azure CLI, ARM templates, or Bicep.

---

## 🔧 **Core Fields for Subnet Creation**

### 1. **Name**

* **Description:** The name of the subnet.
* **Requirements:** Must be unique within the VNet.
* **Example:** `subnet-frontend`, `db-subnet`.

### 2. **Address Range (CIDR Block)**

* **Description:** The IP address range (in CIDR notation) that defines the subnet.
* **Constraints:**

  * Must be a subset of the VNet’s address space.
  * Cannot overlap with other subnets in the VNet.
  * Minimum size: /29 (8 IP addresses); Maximum size: /8.
* **Example:** `10.0.1.0/24`.

---

## 🔒 **Security and Control Settings**

### 3. **Network Security Group (NSG) (Optional)**

* **Description:** An NSG can be associated to control inbound/outbound traffic via rules.
* **Options:**

  * Select an existing NSG.
  * Create a new NSG.
  * Leave unassociated (default allow all).
* **Example Use:** Block SSH from the internet, allow HTTP.

### 4. **Route Table (Optional)**

* **Description:** Custom route table to control traffic routing.
* **Purpose:** Direct traffic to firewalls, VPNs, or other appliances.
* **Example Use:** Route `0.0.0.0/0` to a network virtual appliance.

---

## 🌐 **Service Endpoints and Delegation**

### 5. **Service Endpoints (Optional)**

* **Description:** Enables private connectivity to Azure services (e.g., Azure Storage, SQL).
* **Purpose:** Traffic to selected services remains in the Azure backbone.
* **Example:** Add service endpoints for `Microsoft.Storage`.

### 6. **Subnet Delegation (Optional)**

* **Description:** Assigns the subnet to a specific Azure service.
* **Used For:** Services like Azure App Service Environment, Azure Container Instances, Azure Bastion.
* **Example:** Delegate to `Microsoft.Web/serverFarms`.

---

## 📛 **Private Endpoint Network Policies**

### 7. **Private Endpoint Network Policies**

* **Description:** Controls whether NSG rules apply to private endpoints.
* **Default:** Enabled (policies apply).
* **Option:** Disable if you want private endpoints to bypass NSG for specific scenarios.
* **Common For:** Private Link setups.

---

## 📛 **Private Link Service Network Policies**

### 8. **Private Link Service Network Policies**

* **Description:** Controls NSG enforcement on services that provide Private Link.
* **Default:** Enabled.
* **Typically Required:** To be disabled when setting up Private Link services.

---

## 🔒 **Firewall and DNS Features (Advanced Networking Scenarios)**

### 9. **Integration with Azure Firewall Policies (via Route Tables)**

* While not a direct field in subnet creation, subnets can be later associated with:

  * Azure Firewall via custom UDRs (User-Defined Routes).
  * DNS settings inherited from the VNet or custom per subnet.

---

## ✅ **Best Practices & Notes**

* Reserve IP ranges carefully: First 4 and last IP in subnet are reserved.
* Plan address ranges to avoid overlapping with on-prem networks if using VPN or ExpressRoute.
* Use NSGs for layer 4 security (TCP/UDP port control), not just Azure Firewall.
* When using service delegation, only one delegation per subnet is allowed.

---

## 💡 Example: Azure CLI Command for Subnet Creation

```bash
az network vnet subnet create \
  --name app-subnet \
  --vnet-name myVnet \
  --resource-group myResourceGroup \
  --address-prefix 10.0.2.0/24 \
  --network-security-group myNSG \
  --route-table myRouteTable \
  --service-endpoints Microsoft.Storage \
  --delegations Microsoft.Web/serverFarms
```

---

Let me know if you want a diagram or ARM/Bicep template example to visualize this further.
