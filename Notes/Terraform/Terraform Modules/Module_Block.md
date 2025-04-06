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


