### VM Creation with backen block and public IP block:

```
terraform {
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "4.25.0"
    }
  }
  backend "azurerm" {
    #use_cli              = true                                    
    #use_azuread_auth     = true                                    
    tenant_id            = "628e55e0-ddbc-4fb1-84df-bb0350248525"  
    resource_group_name   = "dkc-rg-01"
    storage_account_name = "dkcstorageaccount001"                              
    container_name       = "dkcstoragecontainer0001"                              
    key                  = "mynewterraform.tfstate"               
  }
}

provider "azurerm" {
  features {}
  subscription_id = "b7df65c6-7c4d-4e35-983d-cd66eea0573a"
}
resource "azurerm_resource_group" "RG-01" {
  name     = "dkc-rg-01"
  location = "West Europe"
}
resource "azurerm_storage_account" "ST-01" {
  depends_on = [ azurerm_resource_group.RG-01 ]
  name                     = "dkcstorageaccount001"
  resource_group_name      = "dkc-rg-01"
  location                 = "West Europe"
  account_tier             = "Standard"
  account_replication_type = "LRS"
}
resource "azurerm_storage_container" "STC-01" {
  depends_on = [ azurerm_resource_group.RG-01, azurerm_storage_account.ST-01 ]
  name                  = "dkcstoragecontainer0001"
  storage_account_id    = azurerm_storage_account.ST-01.id
  container_access_type = "private"
}
resource "azurerm_resource_group" "RG-02" {
  name     = "dkc-rg-02"
  location = "West Europe"
}

resource "azurerm_network_security_group" "NSG-01" {
  name                = "Net-SecG-01"
  location            = azurerm_resource_group.RG-02.location
  resource_group_name = azurerm_resource_group.RG-02.name
}

resource "azurerm_virtual_network" "VN-01" {
  name                = "VNet-01"
  location            = azurerm_resource_group.RG-02.location
  resource_group_name = azurerm_resource_group.RG-02.name
  address_space       = ["10.0.0.0/16"]
  dns_servers         = ["10.0.0.4", "10.0.0.5"]
  }

resource "azurerm_subnet" "int-sub-01" {
  name                 = "inter-subnet-01"
  resource_group_name  = azurerm_resource_group.RG-02.name
  virtual_network_name = azurerm_virtual_network.VN-01.name
  address_prefixes     = ["10.0.3.0/24"]
}
#resource "azurerm_public_ip" "main-pub-ip-01" {                                      #if forgot public ip to define then add this block
 # name                     = "public-ip-01"
  #location                 = azurerm_resource_group.RG-02.location
  #resource_group_name      = azurerm_resource_group.RG-02.name
  #allocation_method        = "Dynamic"  # You can use "Dynamic" if preferred
  #sku                      = "Basic"   # You can change this to "Standard" for more features
#}
resource "azurerm_network_interface" "main-net-01" {
  name                = "nic-01"
  location            = azurerm_resource_group.RG-02.location
  resource_group_name = azurerm_resource_group.RG-02.name

  ip_configuration {
    name                          = "testconfig-01"
    subnet_id                     = azurerm_subnet.int-sub-01.id
    private_ip_address_allocation = "Dynamic"

    #public_ip_address_id          = azurerm_public_ip.main-pub-ip-01.id                    #if forgot public ip to define then add this line with public ip block
    public_ip_address {
      allocation_method = "Dynamic"   # or "Static"
      sku               = "Basic"    # or "Standard"
    }
  }
}

output "vm_public_ip" {
  value = azurerm_public_ip.main-pub-ip-01.ip_address
}

resource "azurerm_virtual_machine" "main-vm" {
  name                  = "vm-01"
  location              = azurerm_resource_group.RG-02.location
  resource_group_name   = azurerm_resource_group.RG-02.name
  network_interface_ids = [azurerm_network_interface.main-net-01.id]
  vm_size               = "Standard_DS1_v2"

  # Uncomment this line to delete the OS disk automatically when deleting the VM
  # delete_os_disk_on_termination = true

  # Uncomment this line to delete the data disks automatically when deleting the VM
  # delete_data_disks_on_termination = true
storage_os_disk {
    name              = "my-os-disk"
    caching           = "ReadWrite"
    create_option     = "FromImage"
  }
storage_image_reference {
    publisher = "MicrosoftWindowsServer"
    offer     = "WindowsServer"
    sku       = "2022-Datacenter"
    version   = "latest"
  }

  os_profile {
    computer_name  = "server-01"
    admin_username = "adminuser"
    admin_password = "password123!"
  }

  os_profile_windows_config {
    provision_vm_agent = true
    enable_automatic_upgrades = true
  }
  tags = {
    environment = "Prod_01"
  }
}

```
