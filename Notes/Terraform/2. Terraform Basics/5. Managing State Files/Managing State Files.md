
## Backend Block:

```
terraform {
  backend "azurerm" {
    #use_cli              = true                                    # Can also be set via `ARM_USE_CLI` environment variable.
    #use_azuread_auth     = true                                    # Can also be set via `ARM_USE_AZUREAD` environment variable.
    tenant_id            = "00000000-0000-0000-0000-000000000000"  # Can also be set via `ARM_TENANT_ID` environment variable. Azure CLI will fallback to use the connected tenant ID if not supplied.
    resource_group_name   = "dkc-rg-01"                            # Can be passed via `-backend-config=`"resource_group_name=<resource group name>"` in the `init` command.
    storage_account_name = "abcd1234"                              # Can be passed via `-backend-config=`"storage_account_name=<storage account name>"` in the `init` command.
    container_name       = "tfstate"                               # Can be passed via `-backend-config=`"container_name=<container name>"` in the `init` command.
    key                  = "prod.terraform.tfstate"                # Can be passed via `-backend-config=`"key=<blob key name>"` in the `init` command.
  }
}
```

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
```







