Bilkul bhai! Ab main tujhe **Terraform ka `output` block** ekdum **asaani se** samjhaata hoon, real **Azure example ke saath**, step-by-step.

---

# 🌟 Terraform `output` Block — Full Explanation in Hindi

## 🔶 Output Block Kya Hota Hai?

`output` block ka use Terraform me **deployment ke baad koi value dikhane** ke liye hota hai.

Ye values helpful hoti hain jab:

* Terraform apply ke baad kuch **important info** chahiye ho (jaise resource ka IP, name, ID)
* Terraform modules ke beech values share karni ho
* Debugging ya logs me kuch check karna ho

---

## 🧱 Basic Syntax

```hcl
output "output_name" {
  value       = <expression>
  description = "Kya value dikha rahe ho"
  sensitive   = true/false   # (optional)
}
```

---

## ✅ Example Without Azure

```hcl
output "region" {
  value       = var.location
  description = "Deployment region"
}
```

---

# 🔷 Azure Example ke Saath

Chalo ek Azure Resource Group aur Virtual Machine ka example lete hain. Ham uske `name`, `id`, aur `public IP` ko output me dikhayenge.

---

## 📁 `main.tf`

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "example" {
  name     = "my-rg"
  location = "East US"
}

resource "azurerm_public_ip" "example" {
  name                = "myPublicIP"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
  allocation_method   = "Dynamic"
}

resource "azurerm_network_interface" "example" {
  name                = "myNIC"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = "<your-subnet-id>"
    private_ip_address_allocation = "Dynamic"
    public_ip_address_id          = azurerm_public_ip.example.id
  }
}

resource "azurerm_linux_virtual_machine" "example" {
  name                = "myVM"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  size                = "Standard_B1s"
  admin_username      = "azureuser"
  network_interface_ids = [
    azurerm_network_interface.example.id,
  ]

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }

  disable_password_authentication = true
}
```

---

## 📁 `outputs.tf`

```hcl
output "resource_group_name" {
  value       = azurerm_resource_group.example.name
  description = "Resource Group ka naam"
}

output "vm_id" {
  value       = azurerm_linux_virtual_machine.example.id
  description = "VM ka Azure Resource ID"
}

output "vm_public_ip" {
  value       = azurerm_public_ip.example.ip_address
  description = "Virtual Machine ka Public IP"
}

output "vm_private_ip" {
  value       = azurerm_network_interface.example.private_ip_address
  description = "VM ka private IP"
}
```

---

## 🖥️ Output Dekhne ka Tarika

Jab tu ye command run karega:

```bash
terraform apply
```

To apply ke end me tera output kuch is tarah dikhega:

```
Outputs:

resource_group_name = "my-rg"
vm_id               = "/subscriptions/xxxx/resourceGroups/my-rg/providers/Microsoft.Compute/virtualMachines/myVM"
vm_private_ip       = "10.0.0.4"
vm_public_ip        = "20.50.30.100"
```

---

## 🧪 Bonus: Sensitive Output

Agar tu kisi secret ya password ko output me dikha raha hai, to use **hide** karne ke liye:

```hcl
output "admin_password" {
  value     = var.admin_password
  sensitive = true
}
```

Apply ke baad terminal me ye value **hide** rahegi.

---

## 📋 Summary

| Field         | Description                                       |
| ------------- | ------------------------------------------------- |
| `value`       | Jo cheez output karni hai                         |
| `description` | Kya meaning hai us output ka (optional)           |
| `sensitive`   | Agar `true`, to output ko terminal me hide karega |

---

Agar tu chahe to mai `module` ke andar output ka use bhi dikha sakta ho, ya specific Azure services (App Service, Function App, etc.) ke output bhi bana ke de sakta ho.

Bata bhai, next kya samjhaun?
