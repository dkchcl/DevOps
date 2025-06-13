

```
resource "azurerm_resource_group" "rg" {
  name     = var.resource_group_name
  location = var.location
}

resource "azurerm_virtual_network" "vnet" {
  name                = var.vnet_name
  address_space       = var.vnet_address_space
  location            = var.location
  resource_group_name = var.resource_group_name

  depends_on = [
    azurerm_resource_group.rg
  ]
}

resource "azurerm_subnet" "subnet" {
  name                 = var.subnet_name
  resource_group_name  = var.resource_group_name
  virtual_network_name = var.vnet_name
  address_prefixes     = var.subnet_address_prefix

  depends_on = [
    azurerm_resource_group.rg,
    azurerm_virtual_network.vnet
  ]
}

resource "azurerm_public_ip" "public_ip" {
  name                = var.public_ip_name
  location            = var.location
  resource_group_name = var.resource_group_name
  allocation_method   = "Dynamic"
  sku                 = "Basic"

  depends_on = [
    azurerm_resource_group.rg
  ]
}

resource "azurerm_network_security_group" "nsg" {
  name                = var.nsg_name
  location            = var.location
  resource_group_name = var.resource_group_name

  depends_on = [
    azurerm_resource_group.rg
  ]
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

  depends_on = [
    azurerm_resource_group.rg,
    azurerm_network_security_group.nsg
  ]
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

depends_on = [
    azurerm_resource_group.rg,
    azurerm_subnet.subnet,
    azurerm_public_ip.public_ip,
    azurerm_subnet_network_security_group_association.nsg_assoc
  ]
}

resource "azurerm_subnet_network_security_group_association" "nsg_assoc" {
  subnet_id                 = azurerm_subnet.subnet.id
  network_security_group_id = azurerm_network_security_group.nsg.id

   depends_on = [
    azurerm_resource_group.rg,
    azurerm_subnet.subnet,
    azurerm_network_security_group.nsg,
    azurerm_network_security_rule.ssh
  ]
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

  depends_on = [
    azurerm_resource_group.rg,
    azurerm_network_interface.nic
  ]
}
```

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

variable "image_publisher" {}

variable "image_offer" {}

variable "image_sku" {}
```

```
resource_group_name   = "dkc-rg-23"
location              = "west us"
vnet_name             = "vnet-01"
vnet_address_space    = ["10.0.0.0/16"]
subnet_name           = "subnet01"
subnet_address_prefix = ["10.0.1.0/24"]
nsg_name              = "nsg01"
public_ip_name        = "pip01"
nic_name              = "nic01"
vm_name               = "dkcvm53355"
vm_size               = "Standard_B1s"
admin_username        = "adminuser"
admin_password        = "P@ssword1234!"
image_publisher       = "Canonical"
image_offer           = "0001-com-ubuntu-server-focal"
image_sku             = "20_04-lts"
```
```
output "vm_public_ip" {
  value = azurerm_public_ip.public_ip.ip_address
}
```



