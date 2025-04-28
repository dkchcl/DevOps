## Validation Block:

**"Validation - A block to define validation rules, usually in addition to type constraints."**

---

### 🔹 **Validation Block** kya hota hai?

Jab hum kisi cheez ka structure define karte hain (jaise kisi form ka ya configuration ka), toh usme sirf ye batana kaafi nahi hota ki value ka type kya hai (jaise string, number, etc.). Uske alawa bhi kuch extra rules chahiye hote hain — **yehi rules validation block me likhe jaate hain.**

---

### 🔹 Example ke sath samjho:

Maan lo tumhare paas ek input field hai jisme user apna **age** bhar raha hai.

Tumne likha:

```hcl
variable "age" {
  type = number
  validation {
    condition     = var.age >= 18 && var.age <= 60
    error_message = "Age must be between 18 and 60."
  }
}
```

---

### ✅ Yahaan kya ho raha hai?

- `type = number` bolta hai ki **sirf number chalega**, strings nahi.
- `validation` block ke andar:
  - `condition`: Ye ek extra rule hai — ki **number 18 se kam ya 60 se zyada nahi hona chahiye**.
  - `error_message`: Agar rule follow nahi hua toh user ko ye error message dikhega.

---

Toh **type constraint** bas ye dekhta hai ki data ka type sahi hai ya nahi.  
Aur **validation block** ensure karta hai ki value logical bhi ho — jaise range me ho, ya kisi condition pe khari utarti ho.

---


## Azure ke example ke sath samjhaate hai. 💙

---

### 🔹 Terraform aur Azure ka context

Maan le hum **Terraform** use kar rahe hain Azure resources create karne ke liye — jaise ki ek **Azure Storage Account**.

Terraform mein hum variables define karte hain taaki unka use infrastructure banaane mein ho sake. Ab un variables ko sirf type se restrict karna kaafi nahi hota, unpe aur bhi **validation rules** lagani padti hain — jaise naam ka format, allowed values, range, etc.

---

#### 🔹 Pehle basic variable samajh:

```hcl
variable "location" {
  type = string
}
```

Ye toh bas bolta hai ki location ek string honi chahiye. Lekin agar koi `"Mars"` ya `"XYZ"` likh de location mein toh?

❌ **Azure valid locations nahi hain**!

---

#### 🔹 Ab validation block ka kaam aata hai:

```hcl
variable "location" {
  type = string

  validation {
    condition = contains([
      "eastus",
      "westus",
      "centralus",
      "eastus2",
      "westeurope",
      "northeurope"
    ], var.location)

    error_message = "Location must be a valid Azure region like eastus, westus, or westeurope."
  }
}
```

---

#### 🔍 Breakdown:

- `type = string`: Bas string hona chahiye.
- `validation`: Ye block extra check laga raha hai.
- `condition`: `contains([...], var.location)` — yeh check karta hai ki jo value user ne di hai wo list of allowed Azure regions me hai ya nahi.
- `error_message`: Agar galat region diya gaya, toh yeh custom message dikhega user ko.

---

### 🔹 Ek aur real-world Azure example:

Let's say, tu ek Azure Storage Account bana raha hai, aur chahta hai ki user sirf allowed replication types hi choose kare.

```hcl
variable "account_replication_type" {
  type = string

  validation {
    condition = can(regex("^(LRS|GRS|RAGRS|ZRS|GZRS|RAGZRS)$", var.account_replication_type))
    error_message = "Replication type must be one of: LRS, GRS, RAGRS, ZRS, GZRS, RAGZRS."
  }
}
```

Yahan pe humne `regex` se check kiya hai ki jo bhi user input kare wo sirf inme se hi koi ek ho: LRS, GRS, etc.

---

## 🔹 Final Touch: Use of this variable

```hcl
resource "azurerm_storage_account" "example" {
  name                     = "mystorageacct123"
  location                 = var.location
  resource_group_name      = azurerm_resource_group.rg.name
  account_tier             = "Standard"
  account_replication_type = var.account_replication_type
}
```

Agar user galat value dega, toh terraform apply ke time pe ruk jaayega aur error dikha dega — thanks to **validation block**.

---

## 🔚 Summary in Simple Words:

| Feature | Kaam |
|--------|------|
| `type` | Bas data ka type check karta hai (string, number, etc.) |
| `validation` | Extra logic daalta hai jaise value range, allowed list, format etc. |
| `error_message` | Custom error message deta hai jab validation fail hoti hai |

---



### Ek AUR Example-

ab main ek **complete Terraform example** de raha hoon jisme hum:

- Azure Resource Group banayenge ✅  
- Azure Storage Account banayenge ✅  
- Aur saath hi variables ka use karenge **type + validation** ke sath 💡

---

## 🔧 Folder structure:
```
azure-storage/
├── main.tf
├── variables.tf
├── terraform.tfvars
```

---

## 📄 `main.tf`

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "example" {
  name     = var.resource_group_name
  location = var.location
}

resource "azurerm_storage_account" "example" {
  name                     = var.storage_account_name
  resource_group_name      = azurerm_resource_group.example.name
  location                 = var.location
  account_tier             = "Standard"
  account_replication_type = var.account_replication_type
}
```

---

## 📄 `variables.tf`

```hcl
variable "location" {
  type = string

  validation {
    condition = contains([
      "eastus", "westus", "centralus", "eastus2", "westeurope", "northeurope"
    ], var.location)

    error_message = "Please enter a valid Azure region like eastus, westus, or westeurope."
  }
}

variable "resource_group_name" {
  type = string

  validation {
    condition     = length(var.resource_group_name) > 2
    error_message = "Resource group name must be at least 3 characters."
  }
}

variable "storage_account_name" {
  type = string

  validation {
    condition = can(regex("^[a-z0-9]{3,24}$", var.storage_account_name))
    error_message = "Storage account name must be lowercase, 3-24 characters, and contain only letters and numbers."
  }
}

variable "account_replication_type" {
  type = string

  validation {
    condition = contains(["LRS", "GRS", "RAGRS", "ZRS", "GZRS", "RAGZRS"], var.account_replication_type)
    error_message = "Replication type must be one of: LRS, GRS, RAGRS, ZRS, GZRS, RAGZRS."
  }
}
```

---

## 📄 `terraform.tfvars`

```hcl
location                = "eastus"
resource_group_name     = "my-rg"
storage_account_name    = "mystorageacct123"
account_replication_type = "LRS"
```

---

## ▶️ Use karne ka tarika:

1. Pehle terminal kholke iss folder mein aa ja:
   ```
   cd azure-storage
   ```

2. Initialize Terraform:
   ```
   terraform init
   ```

3. Dekh le kya banne wala hai:
   ```
   terraform plan
   ```

4. Aur bana de:
   ```
   terraform apply
   ```

---

Agar tu `storage_account_name` mein capital letter dega ya `account_replication_type = "XYZ"` likhega, toh terraform apply fail karega — **isi wajah se validation kaafi important hoti hai.**

---

Bhai, yeh full ka full working example hai. Chahe toh isme aur variables add kar sakte hain — jaise tags, SKU, etc.

Aur koi cheez unclear ho toh poochh lena. Deploy bhi karke dikha doon?
