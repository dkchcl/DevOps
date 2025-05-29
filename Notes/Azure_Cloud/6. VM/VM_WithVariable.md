## **Linux VM Terraform setup** ko pura **variables ke saath** — taaki hum easily value change kar sake bina code ko touch kiye.

Ye setup me hum kar sakta hai:

✅ Values `.tfvars` file se pass karna
✅ Default values rakhna ya CLI se override karna
✅ Reusable & clean structure

---

### 📁 File Structure with Variables

```
terraform-vm/
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
```

---

### 🔹 `main.tf` – All Resources Using Variables

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "rg" {
  name     = var.resource_group_name
  location = var.location
}

resource "azurerm_virtual_network" "vnet" {
  name                = var.vnet_name
  address_space       = [var.vnet_address_space]
  location            = var.location
  resource_group_name = var.resource_group_name

  depends_on = [
    azurerm_resource_group.rg
  ]
}

resource "azurerm_subnet" "subnet" {
  name                 = var.subnet_name
  resource_group_name  = var.resource_group_name
  virtual_network_name = var.vnet_name
  address_prefixes     = [var.subnet_address_prefix]

  depends_on = [
    azurerm_resource_group.rg,
    azurerm_virtual_network.vnet
  ]
}

resource "azurerm_network_security_group" "nsg" {
  name                = var.nsg_name
  location            = var.location
  resource_group_name = var.resource_group_name

  depends_on = [
    azurerm_resource_group.rg
  ]
}

resource "azurerm_network_security_rule" "ssh" {
  name                        = "allow-ssh"
  priority                    = 1001
  direction                   = "Inbound"
  access                      = "Allow"
  protocol                    = "Tcp"
  source_port_range           = "*"
  destination_port_range      = "22"
  source_address_prefix       = "*"
  destination_address_prefix  = "*"
  resource_group_name         = var.resource_group_name
  network_security_group_name = azurerm_network_security_group.nsg.name

  depends_on = [
    azurerm_resource_group.rg,
    azurerm_network_security_group.nsg
  ]
}

resource "azurerm_subnet_network_security_group_association" "nsg_assoc" {
  subnet_id                 = azurerm_subnet.subnet.id
  network_security_group_id = azurerm_network_security_group.nsg.id

  depends_on = [
    azurerm_network_security_rule.ssh
  ]
}

resource "azurerm_public_ip" "public_ip" {
  name                = var.public_ip_name
  location            = var.location
  resource_group_name = var.resource_group_name
  allocation_method   = "Dynamic"
  sku                 = "Basic"

  depends_on = [
    azurerm_resource_group.rg
  ]
}

resource "azurerm_network_interface" "nic" {
  name                = var.nic_name
  location            = var.location
  resource_group_name = var.resource_group_name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "Dynamic"
    public_ip_address_id          = azurerm_public_ip.public_ip.id
  }

  depends_on = [
    azurerm_subnet_network_security_group_association.nsg_assoc
  ]
}

resource "azurerm_linux_virtual_machine" "vm" {
  name                            = var.vm_name
  resource_group_name             = var.resource_group_name
  location                        = var.location
  size                            = var.vm_size
  admin_username                  = var.admin_username
  admin_password                  = var.admin_password
  disable_password_authentication = false

  network_interface_ids = [
    azurerm_network_interface.nic.id,
  ]

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = var.image_publisher
    offer     = var.image_offer
    sku       = var.image_sku
    version   = "latest"
  }

  depends_on = [
    azurerm_network_interface.nic
  ]
}
```

---

### 🔹 `variables.tf` – All Variables Defined

```hcl
variable "resource_group_name" {}
variable "location" {}
variable "vnet_name" {}
variable "vnet_address_space" {}
variable "subnet_name" {}
variable "subnet_address_prefix" {}
variable "nsg_name" {}
variable "public_ip_name" {}
variable "nic_name" {}
variable "vm_name" {}
variable "vm_size" {}
variable "admin_username" {}
variable "admin_password" {}

# Image info
variable "image_publisher" {}
variable "image_offer" {}
variable "image_sku" {}
```

---

### 🔹 `terraform.tfvars` – Your Inputs (Easy to Change)

```hcl
resource_group_name     = "dkc-rg-vm"
location                = "West Europe"
vnet_name               = "vnet-vm-01"
vnet_address_space      = "10.0.0.0/16"
subnet_name             = "subnet-vm"
subnet_address_prefix   = "10.0.2.0/24"
nsg_name                = "vm-nsg"
public_ip_name          = "vm-public-ip"
nic_name                = "vm-nic1"
vm_name                 = "linuxvm"
vm_size                 = "Standard_F2"
admin_username          = "adminuser"
admin_password          = "P@ssw0rd1234!"  # ⚠️ Change in production

# Ubuntu 22.04 LTS Image
image_publisher = "Canonical"
image_offer     = "0001-com-ubuntu-server-jammy"
image_sku       = "22_04-lts"
```

---

### 🔹 `outputs.tf` – Public IP Output

```hcl
output "vm_public_ip" {
  value = azurerm_public_ip.public_ip.ip_address
}
```

---

### ✅ Run Steps

```bash
terraform init
terraform plan -var-file="terraform.tfvars"
terraform apply -var-file="terraform.tfvars"
```

---

### 💡 Ab Tu Easily Ye Kar Sakta Hai:

* Password ya VM size change karna — bas `.tfvars` me value update kar.
* Reuse karna multiple environments ke liye (dev, test, prod).
* Output se public IP dekhna aur `ssh adminuser@<ip>` se login.

---

## BreakDown of Above Terraform Code(VM) ---

Bilkul bhai! Ab main **line-by-line** sab kuch samjhaata hoon: har **resource block ka kaam kya hai**, aur **uske `depends_on` ka logic** kyun use hua hai. Ye code Terraform ka hai jo **Azure me ek Linux VM** bana raha hai, jisme:

* Resource Group
* Virtual Network
* Subnet
* NSG (with SSH rule)
* Public IP
* NIC
* VM

---

## 🔹 1. `azurerm_resource_group` – **Resource Group**

```hcl
resource "azurerm_resource_group" "rg" {
  name     = var.resource_group_name
  location = var.location
}
```

### ✅ Purpose:

Ye Azure me ek **Resource Group** banata hai, jisme sab infrastructure resources organize honge.

### ❌ No `depends_on` needed:

Ye top-level resource hai, kisi aur pe depend nahi karta.

---

## 🔹 2. `azurerm_virtual_network` – **VNet**

```hcl
resource "azurerm_virtual_network" "vnet" {
  ...
  depends_on = [
    azurerm_resource_group.rg
  ]
}
```

### ✅ Purpose:

Azure Virtual Network (VNet) provide karta hai isolated network space jisme VM aur subnet rahenge.

### ✅ `depends_on`:

`resource_group_name = var.resource_group_name` se direct dependency nahi banti, isliye explicitly `depends_on` lagaya gaya taaki **RG banne ke baad hi VNet banega**.

---

## 🔹 3. `azurerm_subnet` – **Subnet**

```hcl
resource "azurerm_subnet" "subnet" {
  ...
  depends_on = [
    azurerm_resource_group.rg,
    azurerm_virtual_network.vnet
  ]
}
```

### ✅ Purpose:

Subnet VNet ke andar ek chhoti network range hai jisme VM ka NIC connect hota hai.

### ✅ `depends_on`:

* RG pe dependent hai kyunki wo use karta hai `resource_group_name`
* VNet pe bhi dependent hai kyunki subnet ko uske andar banana padta hai.

---

## 🔹 4. `azurerm_network_security_group` – **NSG**

```hcl
resource "azurerm_network_security_group" "nsg" {
  ...
  depends_on = [
    azurerm_resource_group.rg
  ]
}
```

### ✅ Purpose:

NSG ek firewall jaisa kaam karta hai — yeh traffic allow/block karta hai.

### ✅ `depends_on`:

RG pe dependent hai, kyunki wo use karta hai `resource_group_name`.

---

## 🔹 5. `azurerm_network_security_rule` – **NSG Rule for SSH**

```hcl
resource "azurerm_network_security_rule" "ssh" {
  ...
  depends_on = [
    azurerm_resource_group.rg,
    azurerm_network_security_group.nsg
  ]
}
```

### ✅ Purpose:

Yeh NSG me ek rule create karta hai jo **SSH (port 22)** allow karta hai.

### ✅ `depends_on`:

* RG pe (kyunki NSG usi me ban raha hai)
* NSG pe (kyunki rule NSG ke andar jaayega)

---

## 🔹 6. `azurerm_subnet_network_security_group_association` – **Subnet ko NSG se link karna**

```hcl
resource "azurerm_subnet_network_security_group_association" "nsg_assoc" {
  ...
  depends_on = [
    azurerm_network_security_rule.ssh
  ]
}
```

### ✅ Purpose:

Yeh NSG ko subnet ke saath **associate** karta hai — tabhi traffic filter hoga.

### ✅ `depends_on`:

NSG aur uska rule pe dependent hai. Pehle rule create ho, fir hi NSG associate ho.

---

## 🔹 7. `azurerm_public_ip` – **Public IP**

```hcl
resource "azurerm_public_ip" "public_ip" {
  ...
  depends_on = [
    azurerm_resource_group.rg
  ]
}
```

### ✅ Purpose:

VM ke liye ek public IP provide karta hai taaki external access ho sake.

### ✅ `depends_on`:

RG pe dependent hai kyunki wahi location aur scope deta hai.

---

## 🔹 8. `azurerm_network_interface` – **NIC (Network Interface)**

```hcl
resource "azurerm_network_interface" "nic" {
  ...
  depends_on = [
    azurerm_subnet_network_security_group_association.nsg_assoc
  ]
}
```

### ✅ Purpose:

NIC subnet + public IP ke through VM ko network se connect karta hai.

### ✅ `depends_on`:

* Subnet pe already implicitly dependent hai.
* Lekin humne `nsg_assoc` pe explicitly depend karaya taaki **NSG apply ho chuke ho subnet pe**.

---

## 🔹 9. `azurerm_linux_virtual_machine` – **Linux VM**

```hcl
resource "azurerm_linux_virtual_machine" "vm" {
  ...
  depends_on = [
    azurerm_network_interface.nic
  ]
}
```

### ✅ Purpose:

Azure VM banaata hai jisme Ubuntu (ya jo bhi image vars me diya ho) chalega.

### ✅ `depends_on`:

NIC pe depend hai — bina network ke VM ready nahi ho sakta.

---

## 🔚 Final Execution Order (Terraform samjhega ye order due to dependencies):

1. `azurerm_resource_group.rg`
2. `azurerm_virtual_network.vnet`
3. `azurerm_subnet.subnet`
4. `azurerm_network_security_group.nsg`
5. `azurerm_network_security_rule.ssh`
6. `azurerm_subnet_network_security_group_association.nsg_assoc`
7. `azurerm_public_ip.public_ip`
8. `azurerm_network_interface.nic`
9. `azurerm_linux_virtual_machine.vm`

---

### 📌 Summary:

| Resource         | Purpose             | Depends On |
| ---------------- | ------------------- | ---------- |
| Resource Group   | Base container      | None       |
| VNet             | Network block       | RG         |
| Subnet           | Subnetwork          | RG, VNet   |
| NSG              | Firewall rules      | RG         |
| NSG Rule         | Allow SSH           | RG, NSG    |
| Subnet-NSG Assoc | Apply NSG to subnet | NSG Rule   |
| Public IP        | External IP         | RG         |
| NIC              | Network connect     | Subnet-NSG |
| VM               | Final compute       | NIC        |

---

Bhai, ye full breakdown tha — ab tu chahe to `terraform apply` confidently chala sakta hai.


