terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "4.23.0"
    }
  }
}

provider "azurerm" {
  features {}
  subscription_id = "7d43afd1-1c03-4477-be93-84f09ad18dda"
  # Configuration options
}
resource "azurerm_resource_group" "tiger_5" {
  name     = "raja5-RG"
  location = "West us"
}
resource "azurerm_storage_account" "tiger_6" {
  name                     = "rajastorage626540"
  resource_group_name      = azurerm_resource_group.tiger_5.name
  location                 = azurerm_resource_group.tiger_5.location
  account_tier             = "Standard"
  account_replication_type = "LRS"
}
resource "azurerm_storage_account" "tiger_7" {
  name                     = "rajastorage00665541"
  resource_group_name      = azurerm_resource_group.tiger_5.name
  location                 = azurerm_resource_group.tiger_5.location
  account_tier             = "Standard"
  account_replication_type = "LRS"
}

resource "azurerm_virtual_network" "tiger_8" {
  name                = "vnet-1"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.tiger_5.location
  resource_group_name = azurerm_resource_group.tiger_5.name
}

resource "azurerm_subnet" "tiger_9" {
  name                 = "subnet-01"
  resource_group_name  = azurerm_resource_group.tiger_5.name
  virtual_network_name = azurerm_virtual_network.tiger_8.name
  address_prefixes     = ["10.0.2.0/24"]
  service_endpoints    = ["Microsoft.Sql", "Microsoft.Storage"]
}

resource "azurerm_storage_account" "tiger_10" {
  name                     = "rajastorage006689089"
  resource_group_name      = azurerm_resource_group.tiger_5.name
  location                 = azurerm_resource_group.tiger_5.location
  account_tier             = "Standard"
  account_replication_type = "LRS"

  network_rules {
    default_action             = "Deny"
    ip_rules                   = ["100.0.0.1"]
    virtual_network_subnet_ids = [azurerm_subnet.tiger_9.id]
  }

  tags = {
    environment = "staging"
  }
}
resource "azurerm_network_interface" "tiger_11" {
  name                = "nic-01"
  location            = azurerm_resource_group.tiger_5.location
  resource_group_name = azurerm_resource_group.tiger_5.name

  ip_configuration {
    name                          = "raj_ip"
    subnet_id                     = azurerm_subnet.tiger_9.id
    private_ip_address_allocation = "Dynamic"
  }
}

resource "azurerm_virtual_machine" "tiger_12" {
  name                  = "rajvm01990033"
  location              = azurerm_resource_group.tiger_5.location
  resource_group_name   = azurerm_resource_group.tiger_5.name
  network_interface_ids = [azurerm_network_interface.tiger_11.id]
  vm_size               = "Standard_DS1_v2"

  # Uncomment this line to delete the OS disk automatically when deleting the VM
  # delete_os_disk_on_termination = true

  # Uncomment this line to delete the data disks automatically when deleting the VM
  # delete_data_disks_on_termination = true

  storage_image_reference {
    publisher = "Canonical"
    offer     = "0001-com-ubuntu-server-jammy"
    sku       = "22_04-lts"
    version   = "latest"
  }
  storage_os_disk {
    name              = "myosdisk1"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Standard_LRS"
  }
  os_profile {
    computer_name  = "rajserver1"
    admin_username = "testadmin"
    admin_password = "Password1234!"
  }
  os_profile_linux_config {
    disable_password_authentication = false
  }
  tags = {
    environment = "staging"
  }
}
resource "azurerm_network_interface" "tiger_14" {
  name                = "nic-02"
  location            = azurerm_resource_group.tiger_5.location
  resource_group_name = azurerm_resource_group.tiger_5.name

  ip_configuration {
    name                          = "raj_ip1"
    subnet_id                     = azurerm_subnet.tiger_9.id
    private_ip_address_allocation = "Dynamic"
  }
}
resource "azurerm_windows_virtual_machine" "tiger_13" {
  name                  = "winvm2390"
  resource_group_name   = azurerm_resource_group.tiger_5.name
  location              = azurerm_resource_group.tiger_5.location
  size                  = "Standard_F2"
  admin_username        = "adminuser"
  admin_password        = "P@$$w0rd1234!"
  network_interface_ids = [azurerm_network_interface.tiger_14.id]

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "MicrosoftWindowsServer"
    offer     = "WindowsServer"
    sku       = "2016-Datacenter"
    version   = "latest"
  }
}
