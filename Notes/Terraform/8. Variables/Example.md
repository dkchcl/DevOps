

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
