

## 1----

```
resource "azurerm_resource_group" "RG" {
    count = 4
  name     = "dev-rg"
  location = "westus"
 }
```
```
PS D:\DevOps Notes\my_codes\Terraform\Module\Variables> terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:  
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.RG[0] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-dev"
    }

  # azurerm_resource_group.RG[1] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-dev"
    }

  # azurerm_resource_group.RG[2] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-dev"
    }

  # azurerm_resource_group.RG[3] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-dev"
    }

Plan: 4 to add, 0 to change, 0 to destroy.
```
## 2---
```
resource "azurerm_resource_group" "RG" {
    count = 4
  name     = count.index
  location = "westus"
 }
```
```
PS D:\DevOps Notes\my_codes\Terraform\Module\Variables> terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:  
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.RG[0] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "0"
    }

  # azurerm_resource_group.RG[1] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "1"
    }

  # azurerm_resource_group.RG[2] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "2"
    }

  # azurerm_resource_group.RG[3] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "3"
    }

Plan: 4 to add, 0 to change, 0 to destroy.
```

## 3---
```
resource "azurerm_resource_group" "RG" {
    count = 4
  name     = "dkc-rg-0${count.index}"
  location = "westus"
 }
```
```
PS D:\DevOps Notes\my_codes\Terraform\Module\Variables> terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:  
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.RG[0] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-00"
    }

  # azurerm_resource_group.RG[1] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-01"
    }

  # azurerm_resource_group.RG[2] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-02"
    }

  # azurerm_resource_group.RG[3] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-03"
    }

Plan: 4 to add, 0 to change, 0 to destroy.
```
## 4---
- variable.tf
```
variable "rg_name" {
    type = list(string)
    default = ["dkc-dev", "dkc-test", "dkc-prod"]
}
variable "rg_location" {
    default = "eastus"
    type = string
}
```
- resource.tf
```
resource "azurerm_resource_group" "RG" {
  name     = var.rg_name[2]
  location = var.rg_location
 }
```
```
PS D:\DevOps Notes\my_codes\Terraform\Module\Variables> terraform plan   

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:  
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.RG will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = "dkc-prod"
    }

Plan: 1 to add, 0 to change, 0 to destroy.
```
## 5---

```
variable "rg_name" {
  description = "Name of the resource group"
  type        = list(any)
  default     = ["dkc-rg-01", "dkc-rg-02", "dkc-rg-03", "dkc-rg-04", "dkc-rg-05"]
}
```
```
resource "azurerm_resource_group" "RG" {
  count    = 4
  name     = var.rg_name[count.index]
  location = "westus"
}
```
```
PS D:\My_Code\Terraform\Variables\RG_Meta> terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.RG[0] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-01"
    }

  # azurerm_resource_group.RG[1] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-02"
    }

  # azurerm_resource_group.RG[2] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-03"
    }

  # azurerm_resource_group.RG[3] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-04"
    }

Plan: 4 to add, 0 to change, 0 to destroy.
```

## 6---

- varialbe.tf
```
variable "rg_name" {
    type = list(string)
    default = ["dkc-dev", "dkc-test", "dkc-prod"]
}
```
- resource.tf
```
resource "azurerm_resource_group" "RG" {
  count = length(var.rg_name)
  name     = var.rg_name[count.index]
  location = var.rg_location
 }
```
```
PS D:\DevOps Notes\my_codes\Terraform\Module\Variables> terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:  
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.RG[0] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = "dkc-dev-01"
    }

  # azurerm_resource_group.RG[1] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = "dkc-test-02"
    }

  # azurerm_resource_group.RG[2] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = "dkc-prod-03"
    }

Plan: 3 to add, 0 to change, 0 to destroy.
```



