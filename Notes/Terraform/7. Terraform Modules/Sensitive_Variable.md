## Sensitive Variable

Azure me agar aap kisi variable ko **sensitive** declare karna chahte ho — jaise ki Terraform ka use kar rahe ho Azure infrastructure banane ke liye — to aapko variable ko define karte waqt `sensitive = true` likhna hota hai.

Yeh example Terraform ka hai, jo Azure ke saath commonly use hota hai:

### 🔐 Sensitive Variable in Terraform:
```hcl
variable "my_secret_password" {
  description = "This is a sensitive password"
  type        = string
  sensitive   = true
}
```

### ✅ Iska use jab aap karenge:
```hcl
resource "azurerm_key_vault_secret" "example" {
  name         = "my-secret"
  value        = var.my_secret_password
  key_vault_id = azurerm_key_vault.example.id
}
```

Agar aap kisi aur Azure tool ya service (like Azure DevOps, ARM templates, Bicep) ke context me poochh rahe ho, to mujhe batana — main uss hisaab se samjha dunga.


### if, Terraform use kar rahe ho?

Perfect! Terraform ke context mein aap variables ko sensitive bana ke unka value accidentally logs, plan output, ya terminal pe print hone se rok sakte ho.

### ✅ Sensitive Variable Declare Karne Ka Sahi Tarika:

#### Step 1: `variables.tf` file me likho:
```hcl
variable "admin_password" {
  description = "The admin password for the virtual machine"
  type        = string
  sensitive   = true
}
```

#### Step 2: `terraform.tfvars` ya CLI ke through value do (lekin dhyan rahe, CLI me dena kam secure hota hai):
```hcl
admin_password = "SuperSecret123!"
```

Ya CLI me:
```bash
terraform apply -var="admin_password=SuperSecret123!"
```

#### Step 3: Jab aap `terraform plan` ya `terraform apply` karoge, output me ye value **nahi** dikhayi degi, jaise:
```
# azurerm_linux_virtual_machine.example will be created
+ admin_password = (sensitive value)
```

Aap chaho to output bhi sensitive bana sakte ho:

```hcl
output "vm_password" {
  value     = var.admin_password
  sensitive = true
}
```

Yeh ensure karega ki password kabhi bhi console pe accidentally leak na ho.

### full example with virtual machine ke saath?

Great! 👌 Yahan ek **full Terraform example** hai jismein:

- Ek Azure Resource Group banate hain
- Ek Azure Virtual Network + Subnet
- Ek Public IP + Network Interface
- Ek Linux Virtual Machine
- Aur sabse important: **Admin password ko sensitive variable ke roop me handle karte hain** ✅

---

### 📁 Folder Structure (suggested):

```
/terraform-azure-vm
  ├── main.tf
  ├── variables.tf
  ├── terraform.tfvars
  └── outputs.tf
```

---

### 🟦 `variables.tf`

```hcl
variable "location" {
  default     = "East US"
  description = "Azure region"
}

variable "resource_group_name" {
  default     = "example-rg"
  description = "Name of the resource group"
}

variable "admin_username" {
  default     = "azureuser"
  description = "Admin username"
  sensitive   = true
}

variable "admin_password" {
  description = "Admin password"
  type        = string
  sensitive   = true
}
```

---

### 🛠️ `main.tf`

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "rg" {
  name     = var.resource_group_name
  location = var.location
}

resource "azurerm_virtual_network" "vnet" {
  name                = "example-vnet"
  address_space       = ["10.0.0.0/16"]
  location            = var.location
  resource_group_name = var.resource_group_name
}

resource "azurerm_subnet" "subnet" {
  name                 = "example-subnet"
  resource_group_name  = var.resource_group_name
  virtual_network_name = azurerm_virtual_network.vnet.name
  address_prefixes     = ["10.0.1.0/24"]
}

resource "azurerm_network_interface" "nic" {
  name                = "example-nic"
  location            = var.location
  resource_group_name = var.resource_group_name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "Dynamic"
  }
}

resource "azurerm_linux_virtual_machine" "vm" {
  name                = "example-vm"
  resource_group_name = var.resource_group_name
  location            = var.location
  size                = "Standard_B1ls"
  admin_username      = var.admin_username
  admin_password      = var.admin_password
  disable_password_authentication = false
  network_interface_ids = [azurerm_network_interface.nic.id]

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
    name                 = "myosdisk1"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }
}
```

---

### 📝 `terraform.tfvars`

```hcl
admin_password = "YourSecurePassword123!"
```

⚠️ Pro tip: Terraform automatically loads this file. Never commit it to git! Use `.gitignore`.

---

### 📤 `outputs.tf`

```hcl
output "vm_username" {
  value = var.admin_username
  sensitive   = true
}

output "vm_password" {
  value     = var.admin_password
  sensitive = true
}
```

---

### 🚀 Run this:

```bash
terraform init
terraform plan
terraform apply
```

Plan aur apply ke output me password nahi dikhega because it's sensitive — exactly what we want for security. 🔐

## Do you also want to add a Network Security Group (NSG) to allow SSH (port 22) for connecting to the VM?

Awesome! 🔐 Let’s add a **Network Security Group (NSG)** with a rule to allow **SSH (port 22)** — and associate it with the subnet or network interface so you can connect to the VM securely via SSH.

---

### 🛡️ Step-by-step: Add NSG and SSH Rule in `main.tf`

---

#### 🔹 1. Create NSG Resource
```hcl
resource "azurerm_network_security_group" "nsg" {
  name                = "example-nsg"
  location            = var.location
  resource_group_name = var.resource_group_name

  security_rule {
    name                       = "AllowSSH"
    priority                   = 1001
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}
```

---

#### 🔹 2. Associate NSG with Network Interface (NIC)
```hcl
resource "azurerm_network_interface_security_group_association" "nsg_assoc" {
  network_interface_id      = azurerm_network_interface.nic.id
  network_security_group_id = azurerm_network_security_group.nsg.id
}
```

> ✅ This ensures the NSG applies directly to the VM's network interface.

---

### ✅ You're all set!

Now after `terraform apply`, you’ll be able to SSH into the VM using the dynamic public IP (from the output), like this:

```bash
ssh azureuser@<public_ip_address>
```

(Replace `azureuser` and use your actual public IP from the Terraform output.)
