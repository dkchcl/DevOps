Bilkul bhai! Neeche main tera **final full Terraform code** de raha hoon — sab kuch hardcoded hai, aur ye include karta hai:

✅ Resource Group
✅ Virtual Network
✅ Subnet
✅ Public IP
✅ Network Interface
✅ Network Security Group (NSG)
✅ NSG Rule to allow SSH (port 22)
✅ NSG-subnet association
✅ Linux VM with password login
✅ Public IP output

---

### ✅ **🔥 Final Full Merged Terraform Code (Hardcoded + SSH Enabled)**

```hcl
resource "azurerm_resource_group" "rg-vm" {
  name     = "dkc-rg-vm"
  location = "West Europe"
}

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

resource "azurerm_linux_virtual_machine" "vm" {
  name                            = "linuxvm"
  resource_group_name             = "dkc-rg-vm"
  location                        = "West Europe"
  size                            = "Standard_F2"
  admin_username                  = "adminuser"
  disable_password_authentication = false
  admin_password                  = "P@ssw0rd1234!"  # ⚠️ Strong password rakhna

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

output "vm_public_ip" {
  value = azurerm_public_ip.public-ip.ip_address
}
```

---

### ✅ SSH Access Kaise Kare:

Terraform apply ke baad:

```bash
ssh adminuser@<output_ip_here>
```

Replace `<output_ip_here>` with the IP shown after `terraform apply`.

---

Bhai agar tu chahta hai main isko `.tf` file structure me split karun (e.g. `main.tf`, `outputs.tf`, `nsg.tf`), to wo bhi kar deta hoon. Let me know!
