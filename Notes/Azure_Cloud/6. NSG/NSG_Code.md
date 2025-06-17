## **Terraform code** to create an **Azure Network Security Group (NSG)** 
---

## 🧾 **Terraform Code: Create Azure NSG**

```hcl
provider "azurerm" {
  features {}
}

# Resource Group
resource "azurerm_resource_group" "example" {
  name     = "example-rg"
  location = "East US"
}

# Network Security Group
resource "azurerm_network_security_group" "example_nsg" {
  name                = "example-nsg"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name

  security_rule {
    name                       = "Allow-SSH"
    priority                   = 100
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }

  security_rule {
    name                       = "Allow-HTTP"
    priority                   = 200
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "80"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }

  security_rule {
    name                       = "Deny-All"
    priority                   = 4096
    direction                  = "Inbound"
    access                     = "Deny"
    protocol                   = "*"
    source_port_range          = "*"
    destination_port_range     = "*"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}
```

---

## ✅ What This Code Does:

* Creates a **Resource Group**.
* Creates an **NSG** with:

  * **Allow SSH (port 22)**
  * **Allow HTTP (port 80)**
  * **Deny all other inbound traffic**

---

## 🔗 How to Use:

1. Save the file as `main.tf`.
2. Run the following commands:

```bash
terraform init
terraform plan
terraform apply
```

---
## **Terraform code**- simple explanation--

---

## 🔧 Code Breakdown: Azure NSG using Terraform

---

### 🔹 **Provider Block**

```hcl
provider "azurerm" {
  features {}
}
```

✅ **Matlab:**
Ye batata hai ki hum **Azure Resource Manager (azurerm)** provider use kar rahe hain.
`features {}` likhna mandatory hai latest Terraform versions ke liye.

---

### 🔹 **Resource Group Create Karna**

```hcl
resource "azurerm_resource_group" "example" {
  name     = "example-rg"
  location = "East US"
}
```

✅ **Matlab:**

* `azurerm_resource_group`: Ye Azure me ek **resource group** banata hai.
* `"example"`: Is resource ka naam (Terraform ke andar use hone wala reference name).
* `name = "example-rg"`: Azure portal me jo naam dikhega resource group ka.
* `location = "East US"`: Region jahan ye resource group create hoga.

---

### 🔹 **NSG (Network Security Group) Banana**

```hcl
resource "azurerm_network_security_group" "example_nsg" {
  name                = "example-nsg"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
```

✅ **Matlab:**

* `azurerm_network_security_group`: NSG resource create karta hai.
* `"example_nsg"`: Terraform reference name.
* `name = "example-nsg"`: Azure portal me jo NSG ka naam dikhega.
* `location = azurerm_resource_group.example.location`: Resource group ka hi location use karo.
* `resource_group_name = azurerm_resource_group.example.name`: NSG ko jis resource group me rakhna hai.

---

## 🔐 Ab NSG ke Rules Define kar rahe hain

---

### ✅ **Allow SSH Rule (Port 22)**

```hcl
  security_rule {
    name                       = "Allow-SSH"
    priority                   = 100
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
```

🔍 **Explanation:**

* `name = "Allow-SSH"`: Rule ka naam.
* `priority = 100`: Sabse pehle ye rule apply hoga (lower number = higher priority).
* `direction = "Inbound"`: Ye rule **andar aane wale traffic** ke liye hai.
* `access = "Allow"`: Is rule me traffic **allow** kiya gaya hai.
* `protocol = "Tcp"`: TCP protocol ke liye rule hai.
* `source_port_range = "*"`: Jo bhi port se traffic aa raha hai, sab allowed.
* `destination_port_range = "22"`: Traffic sirf port **22** (SSH) pe jaa sakta hai.
* `source_address_prefix = "*"`: Sabhi IP addresses se allow hai.
* `destination_address_prefix = "*"`: Kisi bhi Azure VM/NIC ke liye.

---

### ✅ **Allow HTTP Rule (Port 80)**

```hcl
  security_rule {
    name                       = "Allow-HTTP"
    priority                   = 200
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "80"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
```

🔍 **Explanation:**

Ye almost same hai jaise SSH rule, bas yahan:

* `name = "Allow-HTTP"`: HTTP rule hai.
* `priority = 200`: Ye second rule hai.
* `destination_port_range = "80"`: Port 80 ka matlab **HTTP traffic**.

---

### ❌ **Deny All Inbound Rule (Fallback)**

```hcl
  security_rule {
    name                       = "Deny-All"
    priority                   = 4096
    direction                  = "Inbound"
    access                     = "Deny"
    protocol                   = "*"
    source_port_range          = "*"
    destination_port_range     = "*"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}
```

🔍 **Explanation:**

* Ye rule **sabhi inbound traffic ko block** karta hai jo upar wale allowed rules me nahi aata.
* `priority = 4096`: Last me lagega.
* `access = "Deny"`: Traffic **deny** kiya jaa raha hai.
* `protocol = "*"`: All protocols.
* `source/destination = "*"`: Sab jagah se aane wale, sab jagah jaane wale traffic block.

---

## 🧪 Recap:

* Azure me NSG ek firewall jaisa hai.
* Har rule ka priority hota hai.
* Humne SSH (22) aur HTTP (80) allow kiya.
* Baaki sab kuch deny kar diya for safety.

---

