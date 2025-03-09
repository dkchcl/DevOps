
```
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "4.22.0"
    }
  }
}

provider "azurerm" {
  features {}
  subscription_id = "f85ee25f-ffbe-4145-896a-4a245999982e"
}

resource "azurerm_resource_group" "RG21" {
  name     = "RG-dkc05"
  location = "West Europe"
}

resource "azurerm_virtual_network" "RG22" {
  name                = "vnet1"
  location            = azurerm_resource_group.RG21.location
  resource_group_name = azurerm_resource_group.RG21.name
  address_space       = ["10.0.0.0/16"]
}

resource "azurerm_subnet" "RG23" {
  name                 = "subnet1"
  resource_group_name  = azurerm_resource_group.RG21.name
  virtual_network_name = azurerm_virtual_network.RG22.name
  address_prefixes     = ["10.0.1.0/24"]
}

resource "azurerm_network_interface" "RG22" {
  name                = "nic1"
  location            = azurerm_resource_group.RG21.location
  resource_group_name = azurerm_resource_group.RG21.name

  ip_configuration {
    name                          = "internal1"
    subnet_id                     = azurerm_subnet.RG23.id
    private_ip_address_allocation = "Dynamic"
  }
}

resource "azurerm_virtual_machine" "RG24" {
  name                  = "vm1"
  location              = azurerm_resource_group.RG21.location
  resource_group_name   = azurerm_resource_group.RG21.name
  network_interface_ids = [azurerm_network_interface.RG22.id]
  vm_size               = "Standard_DS1_v2"

  storage_os_disk {
    name              = "example-os-disk"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Standard_LRS"
  }

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }

  os_profile {
    computer_name  = "hostname1234"
    admin_username = "adminuser"
    admin_password = "Password1234!"
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}
```
