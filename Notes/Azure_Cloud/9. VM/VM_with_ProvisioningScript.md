## VM With Provisioning Script **NGINX** --

---

## 📁 Final Directory Structure

```
azure-vm-nginx/
├── main.tf
├── variables.tf
├── terraform.tfvars
├── install.sh       <-- NGINX provisioning script
```

---

## ✅ `install.sh` — NGINX Auto Install Script

```bash
#!/bin/bash
apt-get update -y
apt-get install -y nginx
echo "<h1>Welcome to Azure VM - NGINX provisioned by Terraform</h1>" > /var/www/html/index.html
systemctl enable nginx
systemctl start nginx
```

> 🔐 This script is encoded using `filebase64()` in Terraform to pass to the VM.

---

## 🔧 `main.tf` (Fully Updated for NGINX + Password Auth)

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "rg" {
  name     = "dkc-vm-nginx-rg"
  location = "East US"
}

resource "azurerm_virtual_network" "vnet" {
  name                = "vm-vnet"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
}

resource "azurerm_subnet" "subnet" {
  name                 = "vm-subnet"
  resource_group_name  = azurerm_resource_group.rg.name
  virtual_network_name = azurerm_virtual_network.vnet.name
  address_prefixes     = ["10.0.1.0/24"]
}

resource "azurerm_network_security_group" "nsg" {
  name                = "vm-nsg"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name

  security_rule {
    name                       = "SSH"
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
    name                       = "HTTP"
    priority                   = 110
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "80"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}

resource "azurerm_public_ip" "public_ip" {
  name                = "vm-public-ip"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
  allocation_method   = "Dynamic"
  sku                 = "Basic"
}

resource "azurerm_network_interface" "nic" {
  name                = "vm-nic"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "Dynamic"
    public_ip_address_id          = azurerm_public_ip.public_ip.id
  }
}

resource "azurerm_network_interface_security_group_association" "nic_nsg" {
  network_interface_id      = azurerm_network_interface.nic.id
  network_security_group_id = azurerm_network_security_group.nsg.id
}

resource "azurerm_linux_virtual_machine" "vm" {
  name                = "nginx-vm"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
  size                = "Standard_B1s"

  network_interface_ids = [
    azurerm_network_interface.nic.id,
  ]

  admin_username                   = var.admin_username
  admin_password                   = var.admin_password
  disable_password_authentication = false

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
    name                 = "nginx-os-disk"
  }

 source_image_reference {
  publisher = "Canonical"
  offer     = "0001-com-ubuntu-server-focal"
  sku       = "20_04-lts"
  version   = "latest"
}

  provision_vm_agent = true

  custom_data = filebase64("install.sh")
}

output "public_ip_address" {
  value = azurerm_public_ip.public_ip.ip_address
}
```

---

## ⚙️ `variables.tf`

```hcl
variable "admin_username" {
  description = "Admin username for the VM"
  type        = string
  default     = "azureuser"
}

variable "admin_password" {
  description = "Admin password for the VM"
  type        = string
  sensitive   = true
}
```

---

## 🔐 `terraform.tfvars`

```hcl
admin_password = "P@ssword123456"
```

---

## 🚀 Deploy Instructions

```bash
terraform init
terraform plan
terraform apply
```

---

## ✅ Post Deployment Check

1. Output me `public_ip_address` aayega.
2. Visit in browser:

```
http://<public_ip_address>
```

➡ You should see:
`Welcome to Azure VM - NGINX provisioned by Terraform`

---

---

## 🔁 Summary of Flow:

1. Resource Group create hota hai →
2. VNet & Subnet bante hain →
3. Public IP & NIC create hota hai →
4. NSG rules apply hote hain (SSH/HTTP open) →
5. NIC me NSG attach hota hai →
6. VM create hoti hai, NIC se connect hoti hai →
7. VM boot pe provisioning script run hoti hai →
8. Output me public IP milta hai → browser me access karo.

---


