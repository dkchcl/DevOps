## **Azure Virtual Machine (VM)** creation ka pura breakdown — saare required aur optional attributes ke saath & dependencies ka structure --

---

## 🧠 Part 1: Azure Virtual Machine Components & Concepts

Azure pe ek VM banane ke liye kuch core components ki zarurat hoti hai. Ye components milke VM ka full ecosystem banate hain:

---

### 1. **Virtual Network (VNet)**

* **Kya hai**: Azure ka private network jisme VM aur dusre resources communicate karte hain.
* **Required**: ✅
* **Kaam**: Jaise ghar ka main gate — iske andar hi sab kuch hota hai.

---

### 2. **Subnet**

* **Kya hai**: VNet ke andar chhota logical network partition.
* **Required**: ✅
* **Kaam**: Room ke andar ek corner jaise — VM is subnet me place hoti hai.

---

### 3. **Network Security Group (NSG)**

* **Kya hai**: Firewall jaisa hai — inbound & outbound traffic control karta hai.
* **Required**: ❌ (optional, but recommended)
* **Kaam**: Batata hai ki kaunsa traffic allow ya deny karna hai.

---

### 4. **Public IP Address**

* **Kya hai**: Internet se direct access ke liye IP.
* **Required**: ❌ (agar internet access chahiye toh)
* **Kaam**: VM ko world se connect karna.

---

### 5. **Network Interface (NIC)**

* **Kya hai**: VM ka network adapter.
* **Required**: ✅
* **Kaam**: VM ka network se connection NIC se hota hai.

---

### 6. **SSH Key / Username & Password**

* **Kya hai**: Login karne ka tarika.
* **Required**: ✅ (Linux ke liye SSH, Windows ke liye username/password)
* **Kaam**: Security & access control.

---

## 🔗 Dependency Flow (How They Work Together)

```txt
VNet
 └── Subnet
      └── NIC
           ├── NSG (attached here or to subnet)
           ├── Public IP (optional)
           └── Attached to VM
                └── Auth via SSH keys or password
```

---

## ⚙️ Required & Optional VM Attributes in Azure

| Attribute                 | Required  | Description                      |
| ------------------------- | --------- | -------------------------------- |
| `name`                    | ✅         | VM ka naam                       |
| `location`                | ✅         | Azure region                     |
| `resource_group_name`     | ✅         | Resource group                   |
| `network_interface_ids`   | ✅         | NIC se link                      |
| `vm_size`                 | ✅         | e.g. Standard\_B1s               |
| `os_profile`              | ✅         | Username, computer name, etc.    |
| `os_profile_linux_config` | ✅ (Linux) | SSH keys                         |
| `storage_image_reference` | ✅         | OS image (Ubuntu, Windows, etc.) |
| `storage_os_disk`         | ✅         | OS disk config                   |
| `tags`                    | ❌         | Metadata                         |
| `availability_set_id`     | ❌         | HA ke liye                       |
| `boot_diagnostics`        | ❌         | Logs                             |

---

## 🧱 Part 2: Terraform Code to Create Azure VM

```hcl
provider "azurerm" {
  features {}
}

# 1. Resource Group
resource "azurerm_resource_group" "rg" {
  name     = "example-resources"
  location = "East US"
}

# 2. Virtual Network
resource "azurerm_virtual_network" "vnet" {
  name                = "example-vnet"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
}

# 3. Subnet
resource "azurerm_subnet" "subnet" {
  name                 = "example-subnet"
  resource_group_name  = azurerm_resource_group.rg.name
  virtual_network_name = azurerm_virtual_network.vnet.name
  address_prefixes     = ["10.0.1.0/24"]
}

# 4. Public IP
resource "azurerm_public_ip" "public_ip" {
  name                = "example-pip"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
  allocation_method   = "Dynamic"
}

# 5. NSG
resource "azurerm_network_security_group" "nsg" {
  name                = "example-nsg"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name

  security_rule {
    name                       = "SSH"
    priority                   = 1001
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}

# 6. NIC
resource "azurerm_network_interface" "nic" {
  name                = "example-nic"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "Dynamic"
    public_ip_address_id          = azurerm_public_ip.public_ip.id
  }
}

# 7. Associate NSG to NIC
resource "azurerm_network_interface_security_group_association" "nsg_assoc" {
  network_interface_id      = azurerm_network_interface.nic.id
  network_security_group_id = azurerm_network_security_group.nsg.id
}

# 8. Virtual Machine
resource "azurerm_linux_virtual_machine" "vm" {
  name                = "example-vm"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
  size                = "Standard_B1s"
  network_interface_ids = [
    azurerm_network_interface.nic.id,
  ]

  admin_username                  = "azureuser"
  admin_password                  = "P@ssword1234!"  # Use strong password
  disable_password_authentication = false

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
    name                 = "example-osdisk"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }
}
```

---

## 🧾 Explanation of Terraform Code (Line by Line)

| Section                       | Explanation                                                |
| ----------------------------- | ---------------------------------------------------------- |
| **provider**                  | Azure provider set karna                                   |
| **resource\_group**           | Azure resource group banata hai                            |
| **virtual\_network & subnet** | Internal network setup                                     |
| **public\_ip**                | Internet access ke liye IP banata hai                      |
| **nsg**                       | NSG ke through port 22 (SSH) allow karta hai               |
| **nic**                       | VM ka network interface setup karta hai                    |
| **nsg\_assoc**                | NSG ko NIC se associate karta hai                          |
| **linux\_virtual\_machine**   | Final VM create karta hai with image, disk, SSH access etc |

---

## 🛠 Commands to Deploy Terraform Code

```bash
terraform init
terraform plan
terraform apply
```

---

## ✅ Tips

* Terraform me resource ka **order automatic** manage hota hai via references.
* `.tfvars` file me sensitive inputs (e.g. ssh key path, username) rakhna best practice hai.
* Agar VM delete karoge to NIC, NSG, IP etc. bhi delete hone chahiye (ya `depends_on` use karo).

---

Agar tu chaahe to main ye same code **Windows VM ke liye**, ya **multiple VMs with loop**, ya **auto provisioning script** ke sath bhi de sakta hoon.

Bata agar aur bhi detail chahiye ya kisi part me confusion ho 💡
