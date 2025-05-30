## Chalo ek ek block ko **detail mein samajhte hain**, line-by-line:

---

### 🔹 Module: `resource_group`

```hcl
module "resource_group" {
  source = "../Resource_Group"
  resource_group_name = var.resource_group_name
  location = var.location
}
```

✅ **Kya karta hai?**

* Yeh module Azure mein ek **Resource Group** create karta hai.
* `source = "../Resource_Group"` ka matlab hai ki ye module ka code `../Resource_Group` folder mein hai.
* Variables:

  * `resource_group_name`: RG ka naam
  * `location`: RG ki Azure region (e.g., `eastus`)

---

### 🔹 Module: `virtual_network`

```hcl
module "virtual_network" {
  source = "../Virtual_Network"
  depends_on = [ module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  vnet_name = var.vnet_name
  vnet_address_space = var.vnet_address_space 
}
```

✅ **Kya karta hai?**

* Ek **Virtual Network (VNet)** create karta hai.
* `depends_on` ensures ki pehle Resource Group ban jaye.
* `vnet_address_space` jaise: `["10.0.0.0/16"]`

---

### 🔹 Module: `subnet`

```hcl
module "subnet" {
  source = "../Subnet"
  depends_on = [ module.virtual_network ]
  vnet_name = var.vnet_name
  resource_group_name = var.resource_group_name
  subnet_name = var.subnet_name
  subnet_address_prefix = var.subnet_address_prefix
}
```

✅ **Kya karta hai?**

* VNet ke andar ek **Subnet** banata hai.
* Depends on Virtual Network (matlab VNet pehle banna chahiye).
* `subnet_address_prefix`: subnet ke liye address space (e.g., `10.0.1.0/24`)

---

### 🔹 Module: `nsg` (Network Security Group)

```hcl
module "nsg" {
  source = "../NSG"
  depends_on = [ module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  nsg_name = var.nsg_name
}
```

✅ **Kya karta hai?**

* **NSG** banata hai jo ki traffic filtering ke liye use hota hai (firewall jaisa).
* Isme inbound/outbound rules define kiye ja sakte hain.

---

### 🔹 Module: `subnet_nsg_assoc`

```hcl
module "subnet_nsg_assoc" {
  source = "../NSG_Assoc"
  depends_on = [ module.nsg ]
  subnet_id = module.subnet.subnet_id
  nsg_id    = module.nsg.nsg_id
}
```

✅ **Kya karta hai?**

* **NSG ko subnet ke saath associate** karta hai.
* `subnet_id`: jisko NSG lagani hai
* `nsg_id`: jo NSG lagani hai

---

### 🔹 Module: `public_ip`

```hcl
module "public_ip" {
  source = "../Public_IP"
  depends_on = [ module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  public_ip_name = var.public_ip_name
}
```

✅ **Kya karta hai?**

* Ek **Public IP address** allocate karta hai jo VM ko publicly accessible banayega.

---

### 🔹 Module: `nic` (Network Interface)

```hcl
module "nic" {
  source = "../NIC"
  depends_on = [ module.subnet ,module.nsg ]
  resource_group_name = var.resource_group_name
  location = var.location
  nic_name = var.nic_name
  subnet_name = var.subnet_name
  public_ip_name = var.public_ip_name
  subnet_id        = module.subnet.subnet_id
  public_ip_id     = module.public_ip.public_ip_id
}
```

✅ **Kya karta hai?**

* **NIC (Network Interface Card)** create karta hai.
* NIC ka use VM ko subnet aur IP se connect karne ke liye hota hai.
* Is NIC mein public IP bhi attach hota hai, isliye VM internet se accessible hota hai.

---

### 🔹 Module: `vm` (Virtual Machine)

```hcl
module "vm" {
  source = "../Virtual_Machine"
  depends_on = [ module.nic , module.resource_group ]
  resource_group_name = var.resource_group_name
  location = var.location
  nic_name = var.nic_name
  nic_id = module.nic.nic_id
  vm_name = var.vm_name
  vm_size = var.vm_size
  admin_username = var.admin_username
  admin_password = var.admin_password
  image_publisher = var.image_publisher
  image_offer = var.image_offer
  image_sku = var.image_sku
}
```

✅ **Kya karta hai?**

* Azure mein **Virtual Machine** create karta hai.
* Ye NIC ke through subnet se connected hoti hai.
* Image info (e.g., Ubuntu, Windows) `publisher`, `offer`, `sku` se define hota hai.
* Admin credentials: `admin_username` and `admin_password`

---

### 🔹 Output Block

```hcl
output "vm_public_ip" {
  value = module.public_ip.public_ip_address
}
```

✅ **Kya karta hai?**

* Terraform ke output mein VM ka **Public IP address** print karega.
* Useful hai jab aap deployment ke baad IP dekhna chahein.

---

## 🔁 Dependency Graph (Order of Creation)

1. Resource Group
2. VNet
3. Subnet
4. NSG
5. NSG to Subnet Association
6. Public IP
7. NIC (uses subnet & public IP)
8. VM (uses NIC)
9. Output public IP

---

