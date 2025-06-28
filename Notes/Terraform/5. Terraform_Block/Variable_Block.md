##  Terraform Variables --
---

# 🌟 Terraform Variables - Full Guide

## 🧱 1. **String Variable**

### 🔹 Explanation:

Ek normal text value hoti hai — jaise location, name, ID, etc.

```hcl
variable "location" {
  type        = string
  description = "Azure region"
  default     = "East US"
}
```

### 📦 Use:

```hcl
location = var.location
```

---

## 🧱 2. **Number Variable**

### 🔹 Explanation:

Koi bhi number (integer ya float). Jaise: disk size, count, etc.

```hcl
variable "vm_count" {
  type        = number
  description = "Number of VMs"
  default     = 2
}
```

---

## 🧱 3. **Bool (Boolean) Variable**

### 🔹 Explanation:

True ya False value ke liye.

```hcl
variable "enable_monitoring" {
  type        = bool
  default     = true
}
```

---

## 🧱 4. **List (of Strings, Numbers, etc.)**

### 🔹 Explanation:

Ek list of values. Jaise: multiple IPs, zones, tags, etc.

```hcl
variable "address_space" {
  type        = list(string)
  default     = ["10.0.0.0/16", "192.168.0.0/16"]
}
```

### 📦 Use:

```hcl
address_space = var.address_space
```

---

## 🧱 5. **Map (Key-Value pairs)**

### 🔹 Explanation:

Ek dictionary jaisa hota hai — key: value format me.

```hcl
variable "tags" {
  type = map(string)
  default = {
    environment = "dev"
    owner       = "team-a"
  }
}
```

### 📦 Use:

```hcl
tags = var.tags
```

---

## 🧱 6. **Object**

### 🔹 Explanation:

Multiple fields with specific keys (structured data).

```hcl
variable "vm_config" {
  type = object({
    size       = string
    admin_user = string
    os_disk_gb = number
  })
  default = {
    size       = "Standard_B2s"
    admin_user = "azureuser"
    os_disk_gb = 30
  }
}
```

---

## 🧱 7. **Tuple (Mixed-type list)**

### 🔹 Explanation:

List jisme alag-alag type ke values ho sakte hain.

```hcl
variable "example_tuple" {
  type    = tuple([string, number, bool])
  default = ["vm1", 5, true]
}
```

---

# 📘 Azure Full Example with All Types

### 🗂 `variables.tf`

```hcl
variable "location" {
  type        = string
  default     = "East US"
}

variable "vm_count" {
  type    = number
  default = 2
}

variable "enable_monitoring" {
  type    = bool
  default = true
}

variable "address_space" {
  type    = list(string)
  default = ["10.0.0.0/16"]
}

variable "tags" {
  type = map(string)
  default = {
    env  = "test"
    team = "devops"
  }
}

variable "vm_config" {
  type = object({
    size       = string
    admin_user = string
    os_disk_gb = number
  })
  default = {
    size       = "Standard_B2s"
    admin_user = "azureuser"
    os_disk_gb = 30
  }
}
```

---

### 🗂 `main.tf`

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "example" {
  name     = "my-rg"
  location = var.location
  tags     = var.tags
}

resource "azurerm_virtual_network" "example" {
  name                = "my-vnet"
  address_space       = var.address_space
  location            = var.location
  resource_group_name = azurerm_resource_group.example.name
  tags                = var.tags
}

resource "azurerm_linux_virtual_machine" "vm" {
  count               = var.vm_count
  name                = "vm-${count.index}"
  resource_group_name = azurerm_resource_group.example.name
  location            = var.location
  size                = var.vm_config.size
  admin_username      = var.vm_config.admin_user
  network_interface_ids = []

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
    disk_size_gb         = var.vm_config.os_disk_gb
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }

  disable_password_authentication = true

  tags = var.tags
}
```

---

## 📂 terraform.tfvars (optional input values)

```hcl
vm_count = 3

vm_config = {
  size       = "Standard_DS1_v2"
  admin_user = "admin123"
  os_disk_gb = 64
}
```

---

## ✅ Summary Table

| Variable Type | Use Case Example                   |
| ------------- | ---------------------------------- |
| string        | Location, VM name                  |
| number        | Number of VMs, disk size           |
| bool          | Enable/disable monitoring          |
| list          | Address ranges, availability zones |
| map           | Tags, metadata                     |
| object        | VM configuration, nested values    |
| tuple         | Mixed list values (rarely used)    |

---


