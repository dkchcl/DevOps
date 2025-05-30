## VM With Module-


### Root Modules--

**Main.tf**
```
module "resource_group" {
  source = "../Resource_Group"
  resource_group_name = var.resource_group_name
  location = var.location
}

module "virtual_network" {
  source = "../Virtual_Network"
  depends_on = [ module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  vnet_name = var.vnet_name
  vnet_address_space = var.vnet_address_space 
}

module "subnet" {
  source = "../Subnet"
  depends_on = [ module.virtual_network ]
  vnet_name = var.vnet_name
  resource_group_name = var.resource_group_name
  subnet_name = var.subnet_name
  subnet_address_prefix = var.subnet_address_prefix
}

module "nsg" {
  source = "../NSG"
  depends_on = [ module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  nsg_name = var.nsg_name
}

module "subnet_nsg_assoc" {
  source = "../NSG_Assoc"
  depends_on = [ module.nsg ]
  subnet_id = module.subnet.subnet_id
  nsg_id    = module.nsg.nsg_id
}

module "public_ip" {
  source = "../Public_IP"
  depends_on = [ module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  public_ip_name = var.public_ip_name
}
module "nic" {
  source = "../NIC"
  depends_on = [ module.subnet ,module.nsg ]
  resource_group_name = var.resource_group_name
  location = var.location
  nic_name = var.nic_name
  subnet_name = var.subnet_name
  public_ip_name = var.public_ip_name
  subnet_id        = module.subnet.subnet_id
  public_ip_id     = module.public_ip.public_ip_id

}
module "vm" {
  source = "../Virtual_Machine"
  depends_on = [ module.nic , module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  nic_name = var.nic_name
  nic_id = module.nic.nic_id
  vm_name = var.vm_name
  vm_size = var.vm_size
  admin_username = var.admin_username
  admin_password = var.admin_password
  image_publisher = var.image_publisher
  image_offer = var.image_offer
  image_sku = var.image_sku
}

output "vm_public_ip" {
  value = module.public_ip.public_ip_address
}
```
**terraform.tfvars**
```
resource_group_name     = "dkc-vm-rg"
location                = "West Europe"
vnet_name               = "vnet-vm-01"
vnet_address_space      = "10.0.0.0/16"
subnet_name             = "subnet-vm"
subnet_address_prefix   = "10.0.2.0/24"
nsg_name                = "vm-nsg"
public_ip_name          = "vm-public-ip"
nic_name                = "vm-nic1"
vm_name                 = "linuxvm"
vm_size                 = "Standard_F2"
admin_username          = "adminuser"
admin_password          = "P@ssw0rd1234!"  # ⚠️ Change in production

# Ubuntu 22.04 LTS Image
image_publisher = "Canonical"
image_offer     = "0001-com-ubuntu-server-jammy"
image_sku       = "22_04-lts"
```
**variables.tf**
```
variable "resource_group_name" {}
variable "location" {}

variable "vnet_name" {}
variable "vnet_address_space" {}

variable "subnet_name" {}
variable "subnet_address_prefix" {}

variable "nsg_name" {}
variable "public_ip_name" {}
variable "nic_name" {}

variable "vm_name" {}
variable "vm_size" {}
variable "admin_username" {}
variable "admin_password" {}

# Image info
variable "image_publisher" {}
variable "image_offer" {}
variable "image_sku" {}
```
### Child Modules--

**nic_module** - **nic.tf**
```
resource "azurerm_network_interface" "nic" {
  name                = var.nic_name
  location            = var.location
  resource_group_name = var.resource_group_name
  
  ip_configuration {
    name                          = "internal"
    private_ip_address_allocation = "Dynamic"
    subnet_id             = var.subnet_id
    public_ip_address_id  = var.public_ip_id
  }
}
```
**varialbe**
```
variable "resource_group_name" {}
variable "location" {}
variable "nic_name" {}
variable "subnet_name" {}
variable "public_ip_name" {}
variable "subnet_id" {}
variable "public_ip_id" {}
```
**output**
```
output "nic_id" {
  value = azurerm_network_interface.nic.id
}
```
**nsg_module** - **nsg.tf**
```
resource "azurerm_network_security_group" "nsg" {
  name                = var.nsg_name
  location            = var.location
  resource_group_name = var.resource_group_name
}
```
**variable.tf**
```
variable "resource_group_name" {}
variable "location" {}
variable "nsg_name" {}
```
**output.tf**
```
output "nsg_id" {
  value = azurerm_network_security_group.nsg.id
}
```
**nsg_assoc_module** - **nsg_assoc.tf**
```
resource "azurerm_subnet_network_security_group_association" "nsg_assoc" {
  subnet_id                 = var.subnet_id
network_security_group_id = var.nsg_id
}
```
**variable.tf**
```
variable "subnet_id" {}
variable "nsg_id" {}
```
**output_module** - **output.tf**
```
output "vm_public_ip" {
  value = azurerm_public_ip.public_ip.ip_address
}
```
**publicIP_module** - **publicIP.tf**
```
resource "azurerm_public_ip" "public_ip" {
  name                = var.public_ip_name
  location            = var.location
  resource_group_name = var.resource_group_name
  allocation_method   = "Dynamic"
  sku                 = "Basic"
}
```
**variable.tf**
```
variable "resource_group_name" {}
variable "location" {}
variable "public_ip_name" {}
```
**output.tf**
```
output "public_ip_id" {
  value = azurerm_public_ip.public_ip.id
}

output "public_ip_address" {
  value = azurerm_public_ip.public_ip.ip_address
}
```
**resource_group_module** - **resoure.group.tf**
```
resource "azurerm_resource_group" "rg" {
  name     = var.resource_group_name
  location = var.location
}
```
**variable.tf**
```
variable "resource_group_name" {}
variable "location" {}
```
**ssh_module** - **ssh.tf**
```
resource "azurerm_network_security_rule" "ssh" {
  name                        = "allow-ssh"
  priority                    = 1001
  direction                   = "Inbound"
  access                      = "Allow"
  protocol                    = "Tcp"
  source_port_range           = "*"
  destination_port_range      = "22"
  source_address_prefix       = "*"
  destination_address_prefix  = "*"
  resource_group_name         = var.resource_group_name
  network_security_group_name = azurerm_network_security_group.nsg.name
}
```
**variable.tf**
```
variable "resource_group_name" {}
variable "nsg_name" {}
```
**subnet_module** - **subnet.tf**
```
resource "azurerm_subnet" "subnet" {
  name                 = var.subnet_name
  resource_group_name  = var.resource_group_name
  virtual_network_name = var.vnet_name
  address_prefixes     = [var.subnet_address_prefix]
}
```
**variable.tf**
```
variable "resource_group_name" {}
variable "vnet_name" {}
variable "subnet_name" {}
variable "subnet_address_prefix" {}
```
**output.tf**
```
output "subnet_id" {
  value = azurerm_subnet.subnet.id
}
```
**VM_Module** - **vm.tf**
```
resource "azurerm_linux_virtual_machine" "vm" {
  name                            = var.vm_name
  resource_group_name             = var.resource_group_name
  location                        = var.location
  size                            = var.vm_size
  admin_username                  = var.admin_username
  admin_password                  = var.admin_password
  disable_password_authentication = false

  network_interface_ids = [var.nic_id]

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = var.image_publisher
    offer     = var.image_offer
    sku       = var.image_sku
    version   = "latest"
  }
}
```
**variable.tf**
```
variable "resource_group_name" {}
variable "location" {}
variable "nic_name" {}

variable "nic_id" {}
variable "vm_name" {}
variable "vm_size" {}
variable "admin_username" {}
variable "admin_password" {}

# Image info
variable "image_publisher" {}
variable "image_offer" {}
variable "image_sku" {}
```
**virtual_network_module** - **virtual_network.tf**
```
resource "azurerm_virtual_network" "vnet" {
  name                = var.vnet_name
  address_space       = [var.vnet_address_space]
  location            = var.location
  resource_group_name = var.resource_group_name
}
```
**variable.tf**
```
variable "resource_group_name" {}
variable "location" {}
variable "vnet_name" {}
variable "vnet_address_space" {}
```

## **Root modules + Child modules** — ka **line-by-line aur module-by-module explanation**:

---

## 🔷 **Overview**:

Ye Terraform code Azure mein ek **Virtual Machine (VM)** deploy karta hai, uske sath:

* Resource Group
* Virtual Network
* Subnet
* NSG (Network Security Group)
* NSG-Subnet Association
* Public IP
* NIC (Network Interface Card)
* VM

Sab kuch **modular architecture** mein hai — har component ke liye ek **child module** banaya gaya hai.

---

# 🔷 **ROOT MODULE** (`main.tf`)

### ✅ `module "resource_group"` – Resource Group

```hcl
module "resource_group" {
  source = "../Resource_Group"
  resource_group_name = var.resource_group_name
  location = var.location
}
```

➡ Ye module Azure mein ek **resource group** banata hai.
➡ Resource group har resource ko logically group karta hai.

---

### ✅ `module "virtual_network"` – Virtual Network

```hcl
module "virtual_network" {
  source = "../Virtual_Network"
  depends_on = [ module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  vnet_name = var.vnet_name
  vnet_address_space = var.vnet_address_space 
}
```

➡ Ek **VNet** create karta hai jisme VM ka subnet hoga.
➡ VNet address space `10.0.0.0/16` diya gaya hai.
➡ `depends_on` ensure karta hai ki pehle resource group ban jaye.

---

### ✅ `module "subnet"` – Subnet

```hcl
module "subnet" {
  source = "../Subnet"
  depends_on = [ module.virtual_network ]
  vnet_name = var.vnet_name
  resource_group_name = var.resource_group_name
  subnet_name = var.subnet_name
  subnet_address_prefix = var.subnet_address_prefix
}
```

➡ Ye module VNet ke andar **subnet** banata hai.
➡ Subnet ka IP range hai `10.0.2.0/24`.

---

### ✅ `module "nsg"` – Network Security Group

```hcl
module "nsg" {
  source = "../NSG"
  depends_on = [ module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  nsg_name = var.nsg_name
}
```

➡ NSG banata hai jo firewall ki tarah kaam karta hai.
➡ Inbound/Outbound traffic control karta hai.

---

### ✅ `module "subnet_nsg_assoc"` – NSG & Subnet Link

```hcl
module "subnet_nsg_assoc" {
  source = "../NSG_Assoc"
  depends_on = [ module.nsg ]
  subnet_id = module.subnet.subnet_id
  nsg_id    = module.nsg.nsg_id
}
```

➡ NSG ko subnet ke sath associate karta hai — taaki NSG rules apply ho subnet pe.

---

### ✅ `module "public_ip"` – Public IP

```hcl
module "public_ip" {
  source = "../Public_IP"
  depends_on = [ module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  public_ip_name = var.public_ip_name
}
```

➡ Public IP banata hai jisse VM internet se connect ho sake.

---

### ✅ `module "nic"` – Network Interface

```hcl
module "nic" {
  source = "../NIC"
  depends_on = [ module.subnet ,module.nsg ]
  resource_group_name = var.resource_group_name
  location = var.location
  nic_name = var.nic_name
  subnet_name = var.subnet_name
  public_ip_name = var.public_ip_name
  subnet_id        = module.subnet.subnet_id
  public_ip_id     = module.public_ip.public_ip_id
}
```

➡ Ye module **NIC** banata hai — Network Interface, jo VM ko subnet & public IP se connect karta hai.

---

### ✅ `module "vm"` – Virtual Machine

```hcl
module "vm" {
  source = "../Virtual_Machine"
  depends_on = [ module.nic , module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  nic_name = var.nic_name
  nic_id = module.nic.nic_id
  vm_name = var.vm_name
  vm_size = var.vm_size
  admin_username = var.admin_username
  admin_password = var.admin_password
  image_publisher = var.image_publisher
  image_offer = var.image_offer
  image_sku = var.image_sku
}
```

➡ Azure pe **Linux VM create** karta hai.
➡ Isme NIC attach hoti hai, OS image (Ubuntu) set hoti hai, aur credentials diye jate hain.

---

### ✅ Output – VM ka Public IP

```hcl
output "vm_public_ip" {
  value = module.public_ip.public_ip_address
}
```

➡ Ye output dikhata hai VM ka **public IP address** after apply.

---

# 🔷 **CHILD MODULES EXPLAINED**

---

## ✅ 1. `Resource_Group` Module

**File: `resoure.group.tf`**

```hcl
resource "azurerm_resource_group" "rg" {
  name     = var.resource_group_name
  location = var.location
}
```

➡ Azure Resource Group create karta hai.

---

## ✅ 2. `Virtual_Network` Module

```hcl
resource "azurerm_virtual_network" "vnet" {
  name                = var.vnet_name
  address_space       = [var.vnet_address_space]
  location            = var.location
  resource_group_name = var.resource_group_name
}
```

➡ VNet banata hai jisme IP address range define hota hai.

---

## ✅ 3. `Subnet` Module

```hcl
resource "azurerm_subnet" "subnet" {
  name                 = var.subnet_name
  resource_group_name  = var.resource_group_name
  virtual_network_name = var.vnet_name
  address_prefixes     = [var.subnet_address_prefix]
}
```

➡ VNet ke andar Subnet banata hai.

---

## ✅ 4. `NSG` Module

```hcl
resource "azurerm_network_security_group" "nsg" {
  name                = var.nsg_name
  location            = var.location
  resource_group_name = var.resource_group_name
}
```

➡ NSG create karta hai — rules baad mein add kar sakte ho.

---

## ✅ 5. `NSG_Assoc` Module

```hcl
resource "azurerm_subnet_network_security_group_association" "nsg_assoc" {
  subnet_id                 = var.subnet_id
  network_security_group_id = var.nsg_id
}
```

➡ NSG ko Subnet se link karta hai.

---

## ✅ 6. `Public_IP` Module

```hcl
resource "azurerm_public_ip" "public_ip" {
  name                = var.public_ip_name
  location            = var.location
  resource_group_name = var.resource_group_name
  allocation_method   = "Dynamic"
  sku                 = "Basic"
}
```

➡ Dynamic Public IP create karta hai — iska address deploy ke baad milta hai.

---

## ✅ 7. `NIC` Module

```hcl
resource "azurerm_network_interface" "nic" {
  name                = var.nic_name
  location            = var.location
  resource_group_name = var.resource_group_name

  ip_configuration {
    name                          = "internal"
    private_ip_address_allocation = "Dynamic"
    subnet_id                     = var.subnet_id
    public_ip_address_id          = var.public_ip_id
  }
}
```

➡ Network Interface create karta hai jo VM ke IP setup ko manage karta hai. Subnet aur Public IP se linked hota hai.

---

## ✅ 8. `Virtual_Machine` Module

```hcl
resource "azurerm_linux_virtual_machine" "vm" {
  name                            = var.vm_name
  resource_group_name             = var.resource_group_name
  location                        = var.location
  size                            = var.vm_size
  admin_username                  = var.admin_username
  admin_password                  = var.admin_password
  disable_password_authentication = false

  network_interface_ids = [var.nic_id]

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = var.image_publisher
    offer     = var.image_offer
    sku       = var.image_sku
    version   = "latest"
  }
}
```

➡ Actual VM create karta hai Ubuntu OS ke sath.

---

## ✅ 9. `SSH Rule` Module (Optional NSG rule)

```hcl
resource "azurerm_network_security_rule" "ssh" {
  name                        = "allow-ssh"
  priority                    = 1001
  direction                   = "Inbound"
  access                      = "Allow"
  protocol                    = "Tcp"
  source_port_range           = "*"
  destination_port_range      = "22"
  source_address_prefix       = "*"
  destination_address_prefix  = "*"
  resource_group_name         = var.resource_group_name
  network_security_group_name
```

