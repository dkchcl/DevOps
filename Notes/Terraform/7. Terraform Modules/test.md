

## validation Block:


```
# variable "rg_name" {}
# variable "rg_location" {
#     description = "The location where the resource group will be created."
#     type        = string
#     default     = "East US"
# }

variable "rg_name" {
  description = "Name of the resource group"
  type        = string
  default     ="raju-rg"
#   validation {
#     condition     = length(regexall("^[a-z0-9-_]+$", var.rg_name)) > 0
#     error_message = "Resource group name must be lowercase and can include numbers, dashes, and underscores only."
#   }
 validation {
   condition     = can(regex("^[a-z0-9-_]+$", var.rg_name)) && length(var.rg_name) >= 5
   error_message = "Resource group name must be lowercase, at least 3 characters, and can include numbers, dashes, and underscores only."
 }
}


variable "rg_location" {
  description = "Azure region"
  type        = string
  default     ="eastus"
  validation {
    condition     = can(index(["eastus", "westus", "centralus"], var.rg_location) >= 0)
    error_message = "Location must be one of: eastus, westus, centralus"
  }
}
```
## RG Block:

```
resource "azurerm_resource_group" "RG" {
  name     = var.rg_name
  location = var.rg_location
}
```
### Count:
```
resource "azurerm_resource_group" "RG" {
  count = 5 
  name     = "chotu${count.index}"
  location = "westus"
}
```
