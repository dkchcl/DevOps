


## 2.
```
PS D:\My_Code\Terraform\Variables\RG_Meta> terraform apply --auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.RG["dkc-rg-01"] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-01"
    }

  # azurerm_resource_group.RG["dkc-rg-02"] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-02"
    }

  # azurerm_resource_group.RG["dkc-rg-03"] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-03"
    }

  # azurerm_resource_group.RG["dkc-rg-04"] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-04"
    }

  # azurerm_resource_group.RG["dkc-rg-05"] will be created
  + resource "azurerm_resource_group" "RG" {
      + id       = (known after apply)
      + location = "westus"
      + name     = "dkc-rg-05"
    }

Plan: 5 to add, 0 to change, 0 to destroy.
azurerm_resource_group.RG["dkc-rg-01"]: Creating...
azurerm_resource_group.RG["dkc-rg-05"]: Creating...
azurerm_resource_group.RG["dkc-rg-04"]: Creating...
azurerm_resource_group.RG["dkc-rg-02"]: Creating...
azurerm_resource_group.RG["dkc-rg-03"]: Creating...
azurerm_resource_group.RG["dkc-rg-04"]: Still creating... [10s elapsed]
azurerm_resource_group.RG["dkc-rg-05"]: Still creating... [10s elapsed]
azurerm_resource_group.RG["dkc-rg-03"]: Still creating... [10s elapsed]
azurerm_resource_group.RG["dkc-rg-01"]: Still creating... [10s elapsed]
azurerm_resource_group.RG["dkc-rg-02"]: Still creating... [10s elapsed]
azurerm_resource_group.RG["dkc-rg-05"]: Creation complete after 14s [id=/subscriptions/fb85801b-367a-4ef8-8b37-eaf7a1f71813/resourceGroups/dkc-rg-05]
azurerm_resource_group.RG["dkc-rg-03"]: Creation complete after 14s [id=/subscriptions/fb85801b-367a-4ef8-8b37-eaf7a1f71813/resourceGroups/dkc-rg-03]
azurerm_resource_group.RG["dkc-rg-02"]: Creation complete after 15s [id=/subscriptions/fb85801b-367a-4ef8-8b37-eaf7a1f71813/resourceGroups/dkc-rg-02]
azurerm_resource_group.RG["dkc-rg-04"]: Creation complete after 15s [id=/subscriptions/fb85801b-367a-4ef8-8b37-eaf7a1f71813/resourceGroups/dkc-rg-04]
azurerm_resource_group.RG["dkc-rg-01"]: Creation complete after 15s [id=/subscriptions/fb85801b-367a-4ef8-8b37-eaf7a1f71813/resourceGroups/dkc-rg-01]

Apply complete! Resources: 5 added, 0 changed, 0 destroyed.
```
