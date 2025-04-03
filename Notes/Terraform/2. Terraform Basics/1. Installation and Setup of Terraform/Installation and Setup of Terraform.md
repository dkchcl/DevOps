## Installation and Setup of Terraform

Terraform ko install aur set up karne ke liye aapko kuch simple steps follow karne honge. Niche diye gaye steps ko follow karke aap Terraform ko apne system par install kar sakte hain:

### Step 1: Terraform ko Download karo
1. **Terraform ki official website** pe jaake apne operating system ke liye Terraform ka latest version download karo.
   - Terraform ki website: [Terraform Downloads](https://www.terraform.io/downloads.html)
   
2. Apne OS ke hisaab se correct version download karo:
   - **Windows**: `.zip` file
   - **MacOS**: `.zip` file
   - **Linux**: `.zip` ya `.tar.gz` file

### Step 2: Terraform ko Extract karo
1. **Windows**: `.zip` file ko extract karke aapko ek folder milega. Is folder me `terraform.exe` file hogi.
   - Aap ise kisi bhi folder me rakh sakte hain, lekin main aapko recommend karunga ki ise system PATH me add kar lein taki aap command line se Terraform ko easily run kar sakein.

2. **MacOS/Linux**: `.zip` ya `.tar.gz` file ko extract karne ke baad, `terraform` binary file milegi.

### Step 3: PATH ko Configure karo (Optional, but recommended)
1. **Windows**:
   - Apne `terraform.exe` ko ek folder me rakhein (jaise `C:\terraform`).
   - Fir **System Environment Variables** me `PATH` ko update karke is folder ka path add karein:
     - Search for "Environment Variables" in Start menu.
     - Click on "Environment Variables".
     - Under "System Variables", find `Path`, click **Edit**, aur `C:\terraform` ka path add karein.
   
2. **MacOS/Linux**:
   - Apne terminal mein Terraform binary file ko `/usr/local/bin` ya kisi bhi directory jahan aapko binary file ko access karna ho wahan copy kar lein.
   - For example:
     ```bash
     sudo mv terraform /usr/local/bin/
     ```
   - Fir `terraform` command ko terminal mein run karke check karein.

### Step 4: Installation Verify Karein
1. Terminal ya command prompt open karke `terraform` command run karein:
   ```bash
   terraform --version
   ```
   Agar aapko Terraform ka version dikhayi de raha hai, to iska matlab hai ki installation successful ho gaya hai.

### Step 5: Terraform Configuration (First Project Setup)
1. Terraform ka first project setup karne ke liye ek directory banayein aur usme ek `.tf` configuration file banayein. For example:
   ```bash
   mkdir terraform-project
   cd terraform-project
   touch main.tf
   ```
2. `main.tf` file me aap terraform configuration likh sakte hain. Example:
   ```hcl
   provider "aws" {
     region = "us-west-2"
   }

   resource "aws_instance" "example" {
     ami           = "ami-0c55b159cbfafe1f0"
     instance_type = "t2.micro"
   }
   ```

### Step 6: Terraform Commands
1. **Terraform Initialization**:
   Terraform configuration ko initialize karna padta hai:
   ```bash
   terraform init
   ```

2. **Terraform Plan**:
   Jo changes aap deploy karna chahte hain unko review karna:
   ```bash
   terraform plan
   ```

3. **Terraform Apply**:
   Changes ko apply karna:
   ```bash
   terraform apply
   ```

4. **Terraform Destroy**:
   Resources ko destroy karna (jab aapko unko delete karna ho):
   ```bash
   terraform destroy
   ```

Yeh basic setup aur usage tha. Agar aap kisi specific cloud provider (jaise AWS, GCP, Azure) ka use kar rahe hain, to uske liye provider ka configuration setup karna padega, jo Terraform ke documentation me diye gaye hain.
