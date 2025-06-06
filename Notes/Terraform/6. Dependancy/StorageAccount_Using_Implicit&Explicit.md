## Create Storage Account Using Implicit & Explicit Dependancy --

#### Example:(Implicit)
```
terraform {
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "4.25.0"
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
  name                     = "dkcstorageaccount001"
  resource_group_name      = azurerm_resource_group.RG-01.name                             # Implicit dependancy..
  location                 = azurerm_resource_group.RG-01.location                         # Implicit dependancy..
  account_tier             = "Standard"
  account_replication_type = "LRS"
}
resource "azurerm_storage_container" "STC-01" {
  name                  = "dkcstoragecontainer0001"
  storage_account_id    = azurerm_storage_account.ST-01.id
  container_access_type = "private"
}
resource "azurerm_resource_group" "RG-02" {
  name     = "dkc-rg-02"
  location = "West Europe"
}
```

#### Example:(Explicit)

```
terraform {
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "4.25.0"
    }
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
  depends_on = [ azurerm_resource_group.RG-01, azurerm_storage_account.ST-01 ]                        # Explicit dependancy..
  name                  = "dkcstoragecontainer0001"
  storage_account_id    = azurerm_storage_account.ST-01.id
  container_access_type = "private"
}
```
