## Create Azure Storage Account & Containers--

### Azure Storage Account:

#### Using Azure CLI:

#Download & Run the Azure CLI. 

#Run the Azure CLI After installation, close and reopen any active terminal window. Run the Azure CLI with the az command from either Windows Command Prompt or PowerShell. 

**Step 1:** Connect to Your Azure Account You need to authenticate to your Azure account:
```powershell
az login 
```
**Step 2:** A common first step is to check your active subscription. 
```powershell
az account show
```
**Step 3:** Create a Resource Group (if needed) If you don't already have a resource group, you can create one:
```powershell
az group create -Name dineshapirgnew -Location EastUS 
```
**Step 4:** Create a Storage Account (if needed) If you don't already have a storage account, you can create one:
```powershell
az storage account create --name dineshstorage4321 --resource-group dineshapirgnew --location eastus --sku S
tandard_LRS
```
**Result:**

Successfully created.

**Create Azure Containers within Storage Account:**



#### Using Azure Powershell:

Creating a container in an Azure Storage Account using PowerShell is a straightforward process. Here’s a step-by-step guide to help you:

**Step 1:** Install Azure PowerShell Module If you haven't already installed the Azure PowerShell module, you can do so by running the following command:
```powershell
Install-Module -Name Az -AllowClobber -Force 
```
**Step 2:** Connect to Your Azure Account You need to authenticate to your Azure account:
```powershell
Connect-AzAccount 
```
**Step 3:** Create a Resource Group (if needed) If you don't already have a resource group, you can create one:
```powershell
New-AzResourceGroup -Name "myResourceGroup" -Location "EastUS" 
```
**Step 4:** Create a Storage Account (if needed) If you don't already have a storage account, you can create one:
```powershell
New-AzStorageAccount -ResourceGroupName "myResourceGroup" -Name "mystorageaccount" -Location "EastUS" -SkuName "Standard_LRS"
```
**Create Azure Containers within Storage Account --**

Create a Container Now, you can create a container within your storage account:

Get the storage account context
```powershell
$storageAccount = Get-AzStorageAccount -ResourceGroupName "myResourceGroup" -Name "mystorageaccount"
```
```powershell
$ctx = $storageAccount.Context
```
Create the container
```powershell
New-AzStorageContainer -Name "mycontainer" -Context $ctx
```

Feel free to adapt the resource group name, storage account name, and container name to suit your needs. If you encounter any issues, I'm here to help!
