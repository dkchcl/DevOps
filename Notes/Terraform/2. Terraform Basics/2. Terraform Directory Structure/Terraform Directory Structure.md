## Terraform directory structure

Terraform directory structure ka design aapke project ki complexity aur size pe depend karta hai. Yadi aap ek chhoti application bana rahe hain, toh aap simple structure rakh sakte hain, lekin agar project zyada complex hai, toh aapko ek well-organized structure ki zarurat padegi. Terraform ka directory structure modular aur scalable hona chahiye.

Yeh kuch best practices hain jo aap apne Terraform project ke liye follow kar sakte hain:

### 1. **Root Directory**
Root directory mein sabse basic files aur configurations hote hain. Yeh structure simple hota hai aur kisi chhote project ke liye suitable hota hai.

Example:
```
.
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
└── provider.tf
```

- `main.tf`: Ye file aapke infrastructure resources ko define karti hai.
- `variables.tf`: Ye file aapke project ke liye required variables ko define karti hai.
- `outputs.tf`: Ye file aapke infrastructure ke outputs ko define karti hai.
- `terraform.tfvars`: Is file mein aap variables ko assign karte hain (default values).
- `provider.tf`: Is file mein aap provider (AWS, Azure, GCP, etc.) ko configure karte hain.

### 2. **Modular Structure**
Jab project zyada complex ho jaata hai, tab aapko apne resources ko modules mein divide karna chahiye. Isse code reuse, scalability, aur maintainability improve hoti hai.

Example:
```
.
├── main.tf
├── terraform.tfvars
├── variables.tf
├── provider.tf
├── modules/
│   ├── network/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── compute/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── storage/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
└── environments/
    ├── dev/
    │   ├── main.tf
    │   ├── terraform.tfvars
    │   └── variables.tf
    └── prod/
        ├── main.tf
        ├── terraform.tfvars
        └── variables.tf
```

- `modules/`: Is folder mein aap apne reusable components (resources like network, compute, storage) ko organize kar sakte hain.
  - `network/`: Is module mein aap networking resources define karte hain.
  - `compute/`: Is module mein aap compute resources define karte hain.
  - `storage/`: Is module mein aap storage resources define karte hain.
  
- `environments/`: Alag-alag environments ko manage karne ke liye aap separate directories bana sakte hain, jaise dev, prod, stage, etc.
  - `dev/`: Development environment ke liye configuration.
  - `prod/`: Production environment ke liye configuration.

### 3. **Additional Files**
Agar aapko zyada control aur custom configurations chahiye ho, toh kuch aur files bhi use ki ja sakti hain.

- `backend.tf`: Is file mein aap apne backend configurations set karte hain, jaise ki state file ko remote storage mein store karna.
- `provider.tf`: Yeh file provider ko configure karne ke liye hoti hai (e.g., AWS, GCP, Azure).
- `versions.tf`: Ye file aapke Terraform version aur provider versions ko define karti hai.

### Example Full Directory Structure:
```
.
├── main.tf                  # Entry point for defining infrastructure
├── variables.tf             # Declare input variables
├── outputs.tf               # Define outputs
├── terraform.tfvars         # Variable values
├── provider.tf              # Provider configurations
├── versions.tf              # Terraform and provider versions
├── backend.tf               # Remote backend configuration
├── modules/                 # Reusable modules
│   ├── network/
│   ├── compute/
│   └── storage/
├── environments/            # Environment-specific configurations
│   ├── dev/
│   ├── prod/
└── scripts/                 # Custom scripts or local resources (optional)
```

### 4. **State File Handling**
Terraform ka state file `terraform.tfstate` kaafi important hota hai, kyunki ye aapke infrastructure ka current state track karta hai. Aap state ko local ya remote backend (e.g., S3, Azure Blob Storage, etc.) pe store kar sakte hain.

### 5. **Best Practices for Directory Structure**
- **Modularize**: Modules ka use karein taaki code reusability ho aur aapka infrastructure easily manage ho sake.
- **Environment-specific Configurations**: Alag-alag environments ke liye separate directories banayein.
- **Use Remote Backend**: Terraform state ko remote backend pe store karne se team collaboration aur state management asaan ho jaata hai.
- **Separation of Concerns**: Resource types ko logically separate karein (network, compute, storage, etc.).

Is tarah se aap apne Terraform project ko well-structured bana sakte hain, jo ki maintainable, scalable aur manageable ho.
