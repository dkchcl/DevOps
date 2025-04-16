
#### Variables: 



- parent.tf file in parent folder:
   
```
module "azurerm" {
    source = "../resource_group"
    rg_name="RG-2392"
    rg_location="East US"
    }
```


- child.tf file in resource folder:

```
variable "rg_name" {}
variable "rg_location" {}

resource "azurerm_resource_group" "RG-01" {
  name     = var.rg_name
  location = var.rg_location
}
```
