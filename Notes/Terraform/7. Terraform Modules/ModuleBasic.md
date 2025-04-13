

when we are configured module blocks & backend block in configuration file and run terraform init command then happened following:
- Initializing the backend...
- Initializing modules...
- Initializing provider plugins...
- Installing hashicorp/azurerm v4.26.0...
- Terraform created a lock file .terraform.lock.hcl
- Terraform created a directory .terraform
- .terraform contain ---- 1- providers (terraform-provider-azurerm_v4.26.0_x5.exe).,  2- modules (modules.json file)., 3- terraform.tfstate (local copy)file.

**Example-**
```
PS D:\DevOps Notes\my_codes\New folder\Common> terraform init
Initializing the backend...

Successfully configured the backend "azurerm"! Terraform will automatically
use this backend unless the backend configuration changes.
Initializing modules...
- resource-group in ..\azurerm_resource_group
- storage in ..\azurerm_storage_account
Initializing provider plugins...
- Finding hashicorp/azurerm versions matching "4.26.0"...
- Installing hashicorp/azurerm v4.26.0...
- Installed hashicorp/azurerm v4.26.0 (signed by HashiCorp)
Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```




