Sahi hai bhai! Ab main tera code ko **Terraform best practice structure** ke hisaab se multiple `.tf` files mein split kar raha hoon — taaki tera project maintainable aur clean ho jaaye, lekin still **hardcoded** hi rahe (jaise tu chahta hai).

---

### 📁 **Recommended File Structure:**

```
terraform-vm/
│
├── main.tf
├── network.tf
├── nsg.tf
├── vm.tf
├── outputs.tf
```

---

### 🔹 `main.tf` – Resource Group

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "rg-vm" {
  name     = "dkc-rg-vm"
  location = "West Europe"
}
```

---

### 🔹 `network.tf` – VNet, Subnet, Public IP, NIC

```hcl
resource "azurerm_virtual_network" "vnet-vm" {
  name                = "vnet-vm-01"
  address_space       = ["10.0.0.0/16"]
  location            = "West Europe"
  resource_group_name = "dkc-rg-vm"

  depends_on = [
    azurerm_resource_group.rg-vm
  ]
}

resource "azurerm_subnet" "subnet" {
  name                 = "subnet-vm"
  resource_group_name  = "dkc-rg-vm"
  virtual_network_name = "vnet-vm-01"
  address_prefixes     = ["10.0.2.0/24"]

  depends_on = [
    azurerm_virtual_network.vnet-vm
  ]
}

resource "azurerm_public_ip" "public-ip" {
  name                = "vm-public-ip"
  location            = "West Europe"
  resource_group_name = "dkc-rg-vm"
  allocation_method   = "Dynamic"
  sku                 = "Basic"

  depends_on = [
    azurerm_resource_group.rg-vm
  ]
}

resource "azurerm_network_interface" "nic" {
  name                = "vm-nic1"
  location            = "West Europe"
  resource_group_name = "dkc-rg-vm"

  ip_configuration {
    name                          = "internal1"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "Dynamic"
    public_ip_address_id          = azurerm_public_ip.public-ip.id
  }

  depends_on = [
    azurerm_subnet.subnet,
    azurerm_public_ip.public-ip,
    azurerm_resource_group.rg-vm
  ]
}
```

---

### 🔹 `nsg.tf` – NSG, SSH Rule, Association

```hcl
resource "azurerm_network_security_group" "nsg" {
  name                = "vm-nsg"
  location            = "West Europe"
  resource_group_name = "dkc-rg-vm"

  depends_on = [
    azurerm_resource_group.rg-vm
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
  resource_group_name         = "dkc-rg-vm"
  network_security_group_name = azurerm_network_security_group.nsg.name

  depends_on = [
    azurerm_network_security_group.nsg
  ]
}

resource "azurerm_subnet_network_security_group_association" "subnet-nsg" {
  subnet_id                 = azurerm_subnet.subnet.id
  network_security_group_id = azurerm_network_security_group.nsg.id

  depends_on = [
    azurerm_subnet.subnet,
    azurerm_network_security_group.nsg
  ]
}
```

---

### 🔹 `vm.tf` – Linux Virtual Machine

```hcl
resource "azurerm_linux_virtual_machine" "vm" {
  name                            = "linuxvm"
  resource_group_name             = "dkc-rg-vm"
  location                        = "West Europe"
  size                            = "Standard_F2"
  admin_username                  = "adminuser"
  disable_password_authentication = false
  admin_password                  = "P@ssw0rd1234!"  # ⚠️ Strong password rakho

  network_interface_ids = [
    azurerm_network_interface.nic.id,
  ]

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "0001-com-ubuntu-server-jammy"
    sku       = "22_04-lts"
    version   = "latest"
  }

  depends_on = [
    azurerm_network_interface.nic
  ]
}
```

---

### 🔹 `outputs.tf` – Output Public IP

```hcl
output "vm_public_ip" {
  value = azurerm_public_ip.public-ip.ip_address
}
```

---

### 🚀 Usage:

1. Create a folder, e.g. `terraform-vm/`

2. Paste each block into the appropriate `.tf` file.

3. Run:

   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

4. After apply, SSH into the VM:

   ```bash
   ssh adminuser@<public-ip>
   ```

---

Bhai agar tu iske liye `.tfvars` bhi banana chahta hai ya module bana ke reuse karna chahta hai future mein, to bol dena — main wo bhi bana dunga.
