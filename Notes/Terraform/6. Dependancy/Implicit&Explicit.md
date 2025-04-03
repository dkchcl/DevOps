## Terraform Dependency:

Terraform me **dependencies** ka concept bahut important hai, kyunki yeh define karta hai ki resources ke beech kis order me creation aur modification hoga. Jab hum infrastructure manage karte hain, toh resources ek dusre ke saath connected hote hain. Isliye, **dependencies** ka dhyan rakhna zaroori hota hai, taki Terraform ko pata ho ki resources kis order me create honge, modify honge, ya destroy honge.

### Terraform Dependency Management

Terraform **dependencies** ko implicitly aur explicitly handle karta hai:

1. **Implicit Dependencies**: Terraform automatically samajhta hai ki resources kaunse ek dusre se dependent hain. Jaise agar ek resource ka output dusre resource ke input me use ho raha ho, toh Terraform us dependency ko samajh leta hai.
   
2. **Explicit Dependencies**: Agar aapko explicitly dependency define karni ho, toh aap **`depends_on`** argument ka use karte hain. Yeh aapko manually dependency order specify karne ki suvidha deta hai.

---

### 1. **Implicit Dependencies (Automatic Dependency Resolution)**
Terraform apne aap samajh jaata hai ki kis resource ko kiske baad create karna hai, jab ek resource ka output doosre resource ke input me use hota hai. Is case me aapko **`depends_on`** ko explicitly define karne ki zaroorat nahi padti.

#### Example: Implicit Dependency in Azure (Storage Account and Blob Container)

Suppose hum ek **Azure Storage Account** aur usme ek **Blob Container** create karte hain. Blob container ka creation Storage Account ke baad hi hoga, kyunki container ko account me create karna hai. Terraform automatically yeh dependency samajh lega.

```
# Azure Storage Account
resource "azurerm_storage_account" "ST-01" {
  name                     = "dkcstorageaccount001"
  resource_group_name      = azurerm_resource_group.RG-01.name                             # Implicit dependancy..
  location                 = azurerm_resource_group.RG-01.location                         # Implicit dependancy..
  account_tier             = "Standard"
  account_replication_type = "LRS"
}

# Azure Blob Container
resource "azurerm_storage_container" "STC-01" {
  name                  = "dkcstoragecontainer0001"
  storage_account_id    = azurerm_storage_account.ST-01.id                              # This automatically creates a dependency on the Storage Account
  container_access_type = "private"
}
```

### Key Points:
- Yahan **`azurerm_storage_container`** ka `storage_account_name` attribute `azurerm_storage_account.example.name` ko reference kar raha hai.
- Terraform automatically samajh jaata hai ki **Blob Container** ko **Storage Account** ke baad create kiya jaayega.

---

### 2. **Explicit Dependencies (Using `depends_on`)**
Agar aapko kisi specific order me resources create karne ki zaroorat hai, toh aap explicitly **`depends_on`** ka use kar sakte hain. Yeh particularly tab useful hota hai jab indirect dependencies ho ya phir aap chahein ki koi resource specific order me execute ho.

#### Example: Explicit Dependency in Azure (Storage Account and Virtual Network)

Maan lijiye aapko **Azure Virtual Network** create karna hai, aur phir uske baad **Azure Subnet** create karna hai. Subnet ko Virtual Network ke baad hi create karna hoga, toh aap **`depends_on`** ka use karenge.

```hcl
# Azure Virtual Network
resource "azurerm_virtual_network" "VN-01" {
  name                = "vnet-01"
  address_space       = ["10.0.0.0/16"]
  location            = "East US"
  resource_group_name = "dk-rg-01"
}

# Azure Subnet, depends on Virtual Network
resource "azurerm_subnet" "snet-01" {
  name                 = "subnet-01"
  resource_group_name  = "dk-rg-01"
  virtual_network_name = azurerm_virtual_network.VN-01.name
  address_prefixes     = ["10.0.1.0/24"]

  depends_on = [
    azurerm_virtual_network.VN-01  # Explicitly making Subnet dependent on Virtual Network
  ]
}
```

### Key Points:
- **`depends_on`**: Yeh explicitly batata hai ki `azurerm_subnet` resource `azurerm_virtual_network.example` ke baad hi execute hoga.
- Agar **Virtual Network** ready nahi hai, toh **Subnet** create nahi hoga.

---

### 3. **Advanced Dependency Example: Azure Storage Account and Key Vault**
Agar aapko ek **Azure Storage Account** aur ek **Azure Key Vault** create karna hai, aur aap chahte hain ki Key Vault ka creation tab ho jab Storage Account create ho jaye, toh aap dependencies ko explicit tarike se manage kar sakte hain.

#### Example: Azure Storage Account and Key Vault with Dependency
```hcl
# Azure Storage Account
resource "azurerm_storage_account" "ST-01" {
  name                     = "dkcstorageaccount001"
  resource_group_name      = azurerm_resource_group.RG-01.name                             # Implicit dependancy..
  location                 = azurerm_resource_group.RG-01.location                         # Implicit dependancy..
  account_tier             = "Standard"
  account_replication_type = "LRS"
}

# Azure Key Vault, depends on the Storage Account being created
resource "azurerm_key_vault" "KV-01" {
  name                = "keyvault-01"
  location            = "East US"
  resource_group_name = "dk-rg-01"
  sku_name            = "standard"

  depends_on = [
    azurerm_storage_account.ST-01  # Explicit dependency on Storage Account
  ]
}
```

### Key Points:
- **`azurerm_key_vault`** ka creation explicitly `azurerm_storage_account.example` pe depend karega.
- Terraform ko pata chalega ki **Key Vault** ko create karne se pehle **Storage Account** ready hona chahiye.

---

### 4. **Dependency on Outputs**
Kabhi-kabhi aapko output values ko use karte hue dependencies set karni padti hain. Agar ek resource ka output doosre resource ke input me use ho raha ho, toh Terraform apne aap hi dependency create kar leta hai.

#### Example: Output Dependency Between Resources
```hcl
# Azure Storage Account
resource "azurerm_storage_account" "ST-01" {
  name                     = "dkcstorageaccount001"
  resource_group_name      = azurerm_resource_group.RG-01.name                             # Implicit dependancy..
  location                 = azurerm_resource_group.RG-01.location                         # Implicit dependancy..
  account_tier             = "Standard"
  account_replication_type = "LRS"
}

# Output of Storage Account ID
output "storage_account_id" {
  value = azurerm_storage_account.ST-01.id
}

# Azure Resource Group, depends on Storage Account ID
resource "azurerm_resource_group" "RG-01" {
  name     = "dk-rg-01"
  location = "East US"

  tags = {
    storage_account_id = azurerm_storage_account.ST-01.id  # Using Storage Account ID here
  }
}
```

### Key Points:
- **`output` block** ka use karke hum Storage Account ka `id` output me fetch kar rahe hain.
- **Resource Group** ka **`tags`** me Storage Account ka ID store ho raha hai.
- Yeh implicit dependency hai, kyunki Terraform automatically samajhta hai ki Resource Group tabhi create ho sakta hai jab Storage Account create ho jaye.

---

### Conclusion

Terraform me **dependencies** ka management resources ke beech correct order ko ensure karta hai. Dependencies ko handle karne ke liye aap:

- **Implicit dependencies** ka use karte hain jab ek resource ka output doosre resource ke input me use hota hai.
- **Explicit dependencies** ka use karte hain jab aapko manually dependency define karni ho, jaise **`depends_on`**.
- **Outputs** ka use karte hain jab aapko ek resource ka output dusre resource me pass karna ho.

Azure ka example lene se yeh samajh me aata hai ki **Storage Account** aur **Key Vault** ya **Virtual Network** aur **Subnet** ka creation sequence manage karne ke liye dependencies ka sahi tarike se use karna zaroori hai.
