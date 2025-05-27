Bilkul bhai! Ab main tera **Linux VM Terraform setup** ko pura **variables ke saath** bana ke de raha hoon — taaki tu easily value change kar sake bina code ko touch kiye.

Ye setup me tu kar sakta hai:

✅ Values `.tfvars` file se pass karna
✅ Default values rakhna ya CLI se override karna
✅ Reusable & clean structure

---

### 📁 File Structure with Variables

```
terraform-vm/
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
```

---

### 🔹 `main.tf` – All Resources Using Variables

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "rg" {
  name     = var.resource_group_name
  location = var.location
}

resource "azurerm_virtual_network" "vnet" {
  name                = var.vnet_name
  address_space       = [var.vnet_address_space]
  location            = var.location
  resource_group_name = var.resource_group_name
}

resource "azurerm_subnet" "subnet" {
  name                 = var.subnet_name
  resource_group_name  = var.resource_group_name
  virtual_network_name = var.vnet_name
  address_prefixes     = [var.subnet_address_prefix]
}

resource "azurerm_network_security_group" "nsg" {
  name                = var.nsg_name
  location            = var.location
  resource_group_name = var.resource_group_name
}

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

resource "azurerm_subnet_network_security_group_association" "nsg_assoc" {
  subnet_id                 = azurerm_subnet.subnet.id
  network_security_group_id = azurerm_network_security_group.nsg.id
}

resource "azurerm_public_ip" "public_ip" {
  name                = var.public_ip_name
  location            = var.location
  resource_group_name = var.resource_group_name
  allocation_method   = "Dynamic"
  sku                 = "Basic"
}

resource "azurerm_network_interface" "nic" {
  name                = var.nic_name
  location            = var.location
  resource_group_name = var.resource_group_name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "Dynamic"
    public_ip_address_id          = azurerm_public_ip.public_ip.id
  }
}

resource "azurerm_linux_virtual_machine" "vm" {
  name                            = var.vm_name
  resource_group_name             = var.resource_group_name
  location                        = var.location
  size                            = var.vm_size
  admin_username                  = var.admin_username
  admin_password                  = var.admin_password
  disable_password_authentication = false

  network_interface_ids = [
    azurerm_network_interface.nic.id,
  ]

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

---

### 🔹 `variables.tf` – All Variables Defined

```hcl
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

---

### 🔹 `terraform.tfvars` – Your Inputs (Easy to Change)

```hcl
resource_group_name     = "dkc-rg-vm"
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

---

### 🔹 `outputs.tf` – Public IP Output

```hcl
output "vm_public_ip" {
  value = azurerm_public_ip.public_ip.ip_address
}
```

---

### ✅ Run Steps

```bash
terraform init
terraform plan -var-file="terraform.tfvars"
terraform apply -var-file="terraform.tfvars"
```

---

### 💡 Ab Tu Easily Ye Kar Sakta Hai:

* Password ya VM size change karna — bas `.tfvars` me value update kar.
* Reuse karna multiple environments ke liye (dev, test, prod).
* Output se public IP dekhna aur `ssh adminuser@<ip>` se login.

---

Bhai agar tu chahta hai isko aur modular bana ke `modules/` folder me rakhun, to bata — main next level structure bhi bana dunga.
