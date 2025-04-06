## Module_Block ----


- first we create storage account and container for remote state file with below commands:
  
```
az group create -l centralindia -n dkc-state-rg
az storage account create --name dkcstatestrgacct01 --resource-group dkc-state-rg --location centralindia --sku Standard_LRS
az storage container create --account-name dkcstatestrgacct01 --name mystate0190
```

#### Defile Module:

- we define source for each folder child .tf in parent module .tf file.
  
**Example:**

- Create "myrg.tf" in "azurerm_resource_group" folder. (a child module).
```
resource "azurerm_resource_group" "RG-01" {
  name     = "devops-rg-01"
  location = "Central India"
}
```
- Create "mystorage.tf" in "azurerm_storage_account" folder. (a child module).
```
resource "azurerm_storage_account" "ST-01" {
  name                     = "dkcstrgacct0190"
  resource_group_name      = "devops-rg-01"
  location                 = "Central India"
  account_tier             = "Standard"
  account_replication_type = "GRS"
}
```
- Create "main.tf" in "parent_module" folder. (a parent module).
- set source path in parent module's .tf file for child .tf files.
  
```
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "4.26.0"
    }
  }
  backend "azurerm" {
    resource_group_name  = "dkc-state-rg"
    storage_account_name = "dkcstatestrgacct01"
    container_name       = "mystate0190"
    key                  = "dkcstatefile.terraform.tfstate"
  }
}
provider "azurerm" {
  features {}
  subscription_id = "b7df65c6-7c4d-4e35-983d-cd66eea0573a"
}

module "RG-01" {
  source                = "E:\\DevOps Notes\\my_codes\\Terraform\\Module\\azurerm_resource_group"
}
module "ST-01" {
    depends_on = [ module.RG-01 ]
  source                = "E:\\DevOps Notes\\my_codes\\Terraform\\Module\\azurerm_storage_account"
}
```

- after that go parent module path and RUN---
  
```
terraform init
terraform plan 
terraform apply
```

