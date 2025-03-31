## Terraform State Commands:

**Usage:**
```
terraform [global options] state <subcommand> [options] [args]
```
**Subcommands:**
```
    list                List resources in the state
    mv                  Move an item in the state
    pull                Pull current state and output to stdout
    push                Update remote state from a local state file
    replace-provider    Replace provider in the state
    rm                  Remove instances from the state
    show                Show a resource in the state
```


- Terraform ke **state** commands ko samajhna zaroori hai, kyunki ye aapko aapke infrastructure ka track rakhne aur state file ko manage karne me madad karte hain. In commands ka use aap Terraform ke state file ko inspect karne, resources ko modify karne, ya state file ko troubleshoot karne ke liye kar sakte hain.

### Terraform State Commands

Terraform me state commands ka use aap **state file** ko inspect, modify, ya update karne ke liye karte hain. Aap state file ko **locally** ya **remotely** store kar rahe ho, dono cases me ye commands kaafi useful hote hain.

#### 1. **`terraform state list`**
Is command ka use aap apne Terraform state file me stored saare resources ko list karne ke liye karte hain.

**Example:**
Agar aap Azure resources ka management kar rahe hain, to aap ye command run kar sakte hain:
```bash
terraform state list
```

**Output Example:**
```bash
azurerm_storage_account.example
azurerm_storage_container.example
azurerm_virtual_network.example
azurerm_subnet.example
```

Is command se aapko apne **state file** me stored **Azure resources** ke names milenge, jaise storage account, virtual network, subnet, etc.

#### 2. **`terraform state show`**
Is command ka use aap kisi specific resource ke details ko dekhne ke liye karte hain jo state file me stored hai. Iska output resource ke attributes ko display karta hai.

**Example:**
Agar aap **Azure Storage Account** ke details dekhna chahte hain, to ye command run karein:
```bash
terraform state show azurerm_storage_account.example
```

**Output Example:**
```bash
# azurerm_storage_account.example:
resource "azurerm_storage_account" "example" {
    id                            = "/subscriptions/xxxxxx/resourceGroups/example-resources/providers/Microsoft.Storage/storageAccounts/examplestorageacct"
    name                          = "examplestorageacct"
    location                      = "East US"
    resource_group_name           = "example-resources"
    account_tier                   = "Standard"
    account_replication_type      = "LRS"
    primary_web_endpoint          = "https://examplestorageacct.blob.core.windows.net/"
    primary_blob_connection_string = "..."
    ...
}
```

Is output me aapko **storage account** ke details milenge, jaise:
- Resource ID
- Name
- Location
- Replication type
- Web endpoint, etc.

#### 3. **`terraform state rm`**
Is command ka use aap state file me se kisi resource ko **remove** karne ke liye karte hain, bina us resource ko **destroy** kiye. Yeh tab useful hota hai jab aapne manually kisi resource ko delete kiya ho aur aap chahte hain ki Terraform state file se us resource ko remove kar diya jaye.

**Example:**
Agar aap **storage container** ko state file se remove karna chahte hain, to aap is command ka use kar sakte hain:
```bash
terraform state rm azurerm_storage_container.example
```

**Note:** Ye command resource ko state file se remove kar dega, lekin resource ko destroy nahi karega.

#### 4. **`terraform state mv`**
Is command ka use aap ek resource ko ek state file se doosre file me move karne ke liye karte hain. Ye command generally tab use hoti hai jab aapko apne resources ko re-organize karna ho.

**Example:**
Agar aap **azurerm_storage_account** ko apne state file me ek aur location par move karna chahte hain, to aap is command ka use kar sakte hain:
```bash
terraform state mv azurerm_storage_account.example azurerm_storage_account.new_example
```

**Explanation:**
- Yeh command `azurerm_storage_account.example` ko `azurerm_storage_account.new_example` ke naam se move karega state file me.

#### 5. **`terraform state pull`**
Is command ka use aap apne **remote state** ko pull karne ke liye karte hain. Agar aap Azure Blob Storage ya kisi aur remote backend ka use kar rahe hain, to is command se aap state file ko locally fetch kar sakte hain.

**Example:**
```bash
terraform state pull
```

Is command ke baad, aapke pass **state file** ka content local machine par ek output me milega. Agar remote backend me koi update hoti hai, to is command ke zariye aap usko apni local machine par fetch kar sakte hain.

#### 6. **`terraform state push`**
Is command ka use aap apne local state file ko **remote backend** me push karne ke liye karte hain. Yeh command especially useful hoti hai agar aap apne state file ko manually edit karte hain aur fir usko remote storage me push karna chahte hain.

**Example:**
```bash
terraform state push terraform.tfstate
```

Is command ke baad, aapki **local state file** ko remote backend (jaise Azure Blob Storage) me upload kiya jayega.

#### 7. **`terraform state list -state=statefile`**
Agar aap multiple state files ka use kar rahe hain (jaise different environments ke liye), to is command ka use aap specific state file ko list karne ke liye karte hain.

**Example:**
Agar aap ek specific state file `dev.tfstate` ka use karna chahte hain, to aap command likhenge:
```bash
terraform state list -state=dev.tfstate
```

Is command se aapko `dev.tfstate` file me stored resources ki list milegi.

### 8. **State Management with Remote Backends (Azure Example)**

Agar aap **Azure Blob Storage** ka use kar rahe hain Terraform state ko store karne ke liye, to remote backend ke sath state commands ka use kaise hota hai, yeh samajhna zaroori hai.

#### 8.1. **Azure Blob Storage for Remote State**
Remote state ka use karne ke liye aapko backend configuration set karni hoti hai:

**Example (Backend Configuration for Azure Blob Storage):**

```hcl
terraform {
  backend "azurerm" {
    storage_account_name = "examplestorageacct"  # Azure Storage Account Name
    container_name       = "terraform-state"      # Blob Container Name
    key                  = "terraform.tfstate"    # State file name
    resource_group_name  = "example-resources"    # Azure Resource Group Name
  }
}

provider "azurerm" {
  features {}
}
```

**Steps:**
1. Is configuration ke through aap Azure Blob Storage ko backend ke roop me use karte hain, jaha Terraform apna state file store karega.
2. Remote state ko **terraform init** command se initialize kiya jata hai.

```bash
terraform init
```

Jab aap yeh command run karenge, Terraform remote backend (Azure Blob Storage) ko initialize karega aur state file ko securely wahan store karega.

#### 8.2. **State Locking in Remote Backend**
Agar aap remote backend ka use kar rahe hain (for example, Azure Blob Storage), to **state locking** automatically enable ho jata hai, jab aap **state table** ka use karte hain (Azure Table Storage).

Yeh ensure karta hai ki ek samay par sirf ek hi user ya process state file ko modify kare, isse conflicts avoid hote hain.

```hcl
terraform {
  backend "azurerm" {
    storage_account_name = "examplestorageacct"
    container_name       = "terraform-state"
    key                  = "terraform.tfstate"
    resource_group_name  = "example-resources"
    table_name           = "terraform-lock"  # Locking Table for state locking
  }
}
```

### Conclusion

Terraform me **state commands** ka use aap apne infrastructure ko manage karne aur state file ko track karne ke liye karte hain. Azure me agar aap remote state (Azure Blob Storage) ka use kar rahe hain, to aap **state commands** ke saath apne resources ko efficiently inspect, modify, ya move kar sakte hain. Remote state ka use karte hue **state locking** aur **versioning** ka fayda uthana zaruri hota hai, jisse aapka infrastructure manage karna safe aur reliable hota hai.
