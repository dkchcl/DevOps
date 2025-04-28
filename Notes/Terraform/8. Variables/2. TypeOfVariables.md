### 🔹 Types of Variables in Terraform

Terraform me mainly 3 types ke variables hote hain:

| Type             | Use Case                                                  |
|------------------|------------------------------------------------------------|
| **Input Variable** | Aap code ke bahar se value pass karte ho (e.g. VM size) |
| **Local Variable** | Code ke andar hi define karte ho, reuse ke liye         |
| **Output Variable**| Execution ke baad value dikhane ke liye (e.g. IP address) |

---

### 🔹 Azure Cloud Example – Input Variable

#### Step 1: `variables.tf` – Yahan variables define karte hain:

```hcl
variable "location" {
  type    = string
  default = "East US"
}

variable "vm_size" {
  type    = string
  default = "Standard_B1s"
}

variable "resource_group_name" {
  type = string
}
```

#### Step 2: `main.tf` – Variables ko use karte hain:

```hcl
resource "azurerm_resource_group" "example" {
  name     = var.resource_group_name
  location = var.location
}

resource "azurerm_linux_virtual_machine" "example" {
  name                = "examplevm"
  resource_group_name = azurerm_resource_group.example.name
  location            = var.location
  size                = var.vm_size
  admin_username      = "azureuser"
  ...
}
```

#### Step 3: `terraform.tfvars` – Yahan variable ki value dete hain:

```hcl
resource_group_name = "my-rg-dev"
location            = "West Europe"
vm_size             = "Standard_DS1_v2"
```

> ⚙️ Terraform automatically `terraform.tfvars` file ko load karta hai jab aap `terraform apply` karte ho.

---

### 🔹 Benefits of Using Variables

- 💡 Reusability (ek hi code multiple environments ke liye)
- 📦 Maintainability (value change karne ke liye code edit nahi karna padta)
- 🔐 Security (sensitive variables like passwords securely handle kiye ja sakte hain)

---

- Hum **ground level se** aur **real-life example** ke through samjhaate hoon, jaise aap kisi dost ko samjha rahe ho. Terraform variables ko aise samjho jaise programming me functions me parameters pass karte ho – taaki ek hi function baar baar use ho sake alag values ke sath. Same logic Terraform me bhi hai.

---

## 🔥 Terraform Variable – Aasan bhaasha me:

Socho aapko Azure me **VM banana hai**. Ab aap chahte ho ki:

- Kabhi East US me banayein
- Kabhi West Europe me
- Kabhi Standard_B1s size ho, kabhi DS1_v2

Agar aap ye sab har baar manually likhoge, to code repeat hoga aur galtiyan bhi hongi. **Isliye variables ka use karte hain.**

---

## 🎯 Terraform Variable Ka Use 3 Jagah Hota Hai:

### 1. **Define karna** – variables.tf file me
```hcl
variable "location" {
  type        = string
  description = "Azure region"
  default     = "East US"  # optional
}

variable "vm_size" {
  type        = string
  description = "VM size"
}

variable "resource_group_name" {
  type        = string
  description = "Resource Group ka naam"
}
```

---

### 2. **Use karna** – main.tf ya kisi bhi .tf file me

```hcl
resource "azurerm_resource_group" "rg" {
  name     = var.resource_group_name
  location = var.location
}

resource "azurerm_linux_virtual_machine" "vm" {
  name                = "myVM"
  resource_group_name = azurerm_resource_group.rg.name
  location            = var.location
  size                = var.vm_size
  admin_username      = "azureuser"
  ...
}
```

> `var.variable_name` likh ke variable ki value use karte hain.

---

### 3. **Value dena** – terraform.tfvars ya CLI se

#### ✅ Option 1: `terraform.tfvars` file
```hcl
resource_group_name = "rg-dev"
location            = "West Europe"
vm_size             = "Standard_DS1_v2"
```

#### ✅ Option 2: CLI se directly
```bash
terraform apply -var="location=West Europe" -var="vm_size=Standard_DS1_v2"
```

---

## 🧠 Ek Real-Life Analogy

Socho aap pizza bana rahe ho 🍕, aur aap ek recipe bana lete ho:

```text
Dough: {{dough_type}}
Toppings: {{toppings}}
Size: {{pizza_size}}
```

Ab aap har baar bas `variables` me values daalte jao:
```text
dough_type = "Thin Crust"
toppings = "Cheese, Olives"
pizza_size = "Medium"
```

Recipe wahi, values alag — same Terraform ka concept hai!

---

## 💎 Bonus: Sensitive Variables (like password)
```hcl
variable "admin_password" {
  type      = string
  sensitive = true
}
```
Ye jab output hoga ya logs me dikhega to **hide** rahega for security. 😎

---

## 📦 Summary (Shortcut yaad rakhne ke liye)

| Step      | File           | Example                         |
|-----------|----------------|----------------------------------|
| Define    | `variables.tf` | `variable "vm_size" { ... }`    |
| Use       | `main.tf`      | `size = var.vm_size`            |
| Assign    | `terraform.tfvars` | `vm_size = "Standard_DS1_v2"` |

---
