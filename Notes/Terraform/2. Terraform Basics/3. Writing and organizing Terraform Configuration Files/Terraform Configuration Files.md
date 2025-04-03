## Terraform configuration

Terraform configuration files ka role aapke infrastructure ko define karna aur manage karna hota hai. Ye files HCL (HashiCorp Configuration Language) mein likhi jaati hain, jo ki human-readable aur declarative language hai. Terraform configuration files aapke resources, providers, variables, outputs, aur state management ko define karte hain.

### Terraform Configuration Files Types:
1. **Main Configuration Files**
2. **Variables Files**
3. **Output Files**
4. **Provider Files**
5. **State Files**
6. **Backend Configuration Files**

#### 1. **Main Configuration Files (e.g., `main.tf`)**
Main configuration files wo files hoti hain jisme aap apne infrastructure resources define karte hain. Isme aap Terraform ke resources (e.g., AWS EC2 instances, GCP buckets) ko specify karte hain.

**Example (`main.tf`):**
```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```

- **Provider Block**: Provider block mein aap apne infrastructure ka provider (e.g., AWS, GCP, Azure) define karte hain.
  - `provider "aws"`: Yeh specify karta hai ki aap AWS ko use kar rahe hain.
  - `region = "us-west-2"`: AWS region define karta hai.

- **Resource Block**: Resource block mein aap infrastructure resources (e.g., EC2 instances, S3 buckets) define karte hain.
  - `resource "aws_instance" "example"`: Yeh AWS EC2 instance ko define karta hai.
  - `ami`: EC2 instance ka Amazon Machine Image (AMI) ID.
  - `instance_type`: EC2 instance ka type, jaise `t2.micro`.

#### 2. **Variables Files (e.g., `variables.tf`)**
Variables files mein aap input variables ko declare karte hain jo Terraform configuration ko flexible banaate hain. Aap variables ka use karte hain to customize aapke resources ke properties without hardcoding values.

**Example (`variables.tf`):**
```hcl
variable "instance_type" {
  description = "The type of the instance"
  type        = string
  default     = "t2.micro"
}

variable "ami" {
  description = "AMI ID for the instance"
  type        = string
}
```

- **`variable "instance_type"`**: Yeh variable declare karta hai, jisme aap instance type specify kar sakte hain. Aap `default` value bhi de sakte hain, ya toh user se input le sakte hain.
- **`ami`**: Yeh variable aapko AMI ID pass karne ke liye request karega. Iska default value nahi diya gaya, isliye Terraform aap se is variable ko set karne ke liye kahega.

Variables ka use aap `main.tf` ya kisi aur configuration file mein kar sakte hain.

#### 3. **Output Files (e.g., `outputs.tf`)**
Output files mein aap apne infrastructure ke output values ko declare karte hain jo aapke resources ko apply karne ke baad show hote hain. Ye outputs typically resource properties jaise IP addresses, URLs, aur other important information hote hain jo users ko chahiye hote hain.

**Example (`outputs.tf`):**
```hcl
output "instance_public_ip" {
  value = aws_instance.example.public_ip
}

output "instance_id" {
  value = aws_instance.example.id
}
```

- **`output "instance_public_ip"`**: Yeh output AWS EC2 instance ka public IP address show karega.
- **`output "instance_id"`**: Yeh output EC2 instance ka ID show karega.

Isse aapko infrastructure create hone ke baad important information mil jaati hai, jo aap further use kar sakte hain ya log kar sakte hain.

#### 4. **Provider Files (e.g., `provider.tf`)**
Provider files mein aap apne infrastructure ke liye provider ko configure karte hain. Provider Terraform ko batata hai ki kis platform (AWS, Azure, GCP) par aap resources create karna chahte hain.

**Example (`provider.tf`):**
```hcl
provider "aws" {
  access_key = "your-access-key"
  secret_key = "your-secret-key"
  region     = "us-west-2"
}
```

- **`provider "aws"`**: Yeh AWS provider ko configure karta hai. Aap apna AWS access key, secret key aur region define karte hain, jisme Terraform AWS resources create karega.

Aap multiple providers ko configure kar sakte hain agar aap multiple cloud platforms (e.g., AWS aur GCP) ka use kar rahe hain.

#### 5. **State Files (e.g., `terraform.tfstate`)**
Terraform state files kaafi important hote hain, kyunki yeh aapke infrastructure ke current state ko track karte hain. Yeh file aapke resources ke actual state ko store karti hai (jaise ki AWS EC2 instance ka ID, public IP, etc.).

- **Local State**: By default, Terraform state local file (`terraform.tfstate`) mein store hoti hai. 
- **Remote State**: Larger teams aur environments ke liye, state ko remote storage (e.g., AWS S3) pe store karna better hota hai taaki state centralized ho aur multiple users state ko access kar sakein.

**Example (Remote State in `backend.tf`):**
```hcl
terraform {
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "prod/terraform.tfstate"
    region = "us-west-2"
  }
}
```

#### 6. **Backend Configuration Files (e.g., `backend.tf`)**
Jab aap remote state use karte hain (jaise AWS S3), toh aapko backend configuration ki zarurat hoti hai, jo state file ko store karne ke liye backend configure karta hai.

**Example (`backend.tf`):**
```hcl
terraform {
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "prod/terraform.tfstate"
    region = "us-west-2"
  }
}
```

- **`backend "s3"`**: Yeh backend configuration ko define karta hai jo Terraform state ko S3 bucket mein store karega.
- **`bucket`**: Yeh S3 bucket ka naam hai jisme state file store hogi.
- **`key`**: Yeh file path hai jo state ko identify karta hai.

---

### Summary of Key Terraform Configuration Files:

| File Type           | Purpose                                                                                       | Example Content                                          |
|---------------------|-----------------------------------------------------------------------------------------------|----------------------------------------------------------|
| **`main.tf`**        | Resources define karte hain, jaise EC2 instances, storage, networks, etc.                    | `resource "aws_instance" "example" {...}`                |
| **`variables.tf`**   | Variables define karte hain, jo configuration ko customize karte hain.                        | `variable "instance_type" {...}`                         |
| **`outputs.tf`**     | Output values define karte hain, jo applied infrastructure ka result hote hain.               | `output "instance_public_ip" {...}`                      |
| **`provider.tf`**    | Providers (AWS, Azure, etc.) ko configure karte hain.                                         | `provider "aws" {...}`                                   |
| **`terraform.tfvars`**| Variables ke actual values define karte hain jo Terraform apply ke time pe use hoti hain.      | `region = "us-west-2"`                                    |
| **`backend.tf`**     | Remote backend configuration define karta hai (e.g., S3, Azure Blob Storage).                | `terraform { backend "s3" {...} }`                       |
| **State File**       | Terraform ke state ko store karta hai, jo resources ke actual state ko track karta hai.       | `terraform.tfstate` (automatically created by Terraform) |

---

In configuration files ka use karke aap apne infrastructure ko declaratively define kar sakte hain, jo ki Terraform ke through automatically provision ho sakta hai. Ye files modular aur reusable hote hain, aur aapko apne infrastructure ko manage karna kaafi asaan banata hai.
