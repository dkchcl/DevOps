## Create Azure Storage Account & Containers--

### Azure Storage Account:

**Using Azure CLI:**

#Run the Azure CLI 

#Run the Azure CLI After installation, close and reopen any active terminal window. Run the Azure CLI with the az command from either Windows Command Prompt or PowerShell. A common first step is to check your active subscription. 
```powershell
az account show
```
**Step 1:** Install Azure PowerShell Module If you haven't already installed the Azure PowerShell module, you can do so by running the following command:
```powershell
I
```
**Step 2:** Connect to Your Azure Account You need to authenticate to your Azure account:
```powershell
az login 
```
**Step 3:** Create a Resource Group (if needed) If you don't already have a resource group, you can create one:
```powershell
az group create -Name myResourceGroup -Location EastUS 
```
**Step 4:** Create a Storage Account (if needed) If you don't already have a storage account, you can create one:
```powershell
az storage account create --name dineshstorage4321 --resource-group dineshapirgnew --location eastus --sku S
tandard_LRS
```
**Result:**
```powershell
{
  "accessTier": "Hot",
  "accountMigrationInProgress": null,
  "allowBlobPublicAccess": false,
  "allowCrossTenantReplication": false,
  "allowSharedKeyAccess": null,
  "allowedCopyScope": null,
  "azureFilesIdentityBasedAuthentication": null,
  "blobRestoreStatus": null,
  "creationTime": "2025-02-21T09:28:56.468356+00:00",
  "customDomain": null,
  "defaultToOAuthAuthentication": null,
  "dnsEndpointType": null,
  "enableExtendedGroups": null,
  "enableHttpsTrafficOnly": true,
  "enableNfsV3": null,
  "encryption": {
    "encryptionIdentity": null,
    "keySource": "Microsoft.Storage",
    "keyVaultProperties": null,
    "requireInfrastructureEncryption": null,
    "services": {
      "blob": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2025-02-21T09:28:56.593355+00:00"
      },
      "file": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2025-02-21T09:28:56.593355+00:00"
      },
      "queue": null,
      "table": null
    }
  },
  "extendedLocation": null,
  "failoverInProgress": null,
  "geoReplicationStats": null,
  "id": "/subscriptions/f85ee25f-ffbe-4145-896a-4a245999982e/resourceGroups/dineshapirgnew/providers/Microsoft.Storage/storageAccounts/dineshstorage4321",
  "identity": null,
  "immutableStorageWithVersioning": null,
  "isHnsEnabled": null,
  "isLocalUserEnabled": null,
  "isSftpEnabled": null,
  "isSkuConversionBlocked": null,
  "keyCreationTime": {
    "key1": "2025-02-21T09:28:56.593355+00:00",
    "key2": "2025-02-21T09:28:56.593355+00:00"
  },
  "keyPolicy": null,
  "kind": "StorageV2",
  "largeFileSharesState": null,
  "lastGeoFailoverTime": null,
  "location": "eastus",
  "minimumTlsVersion": "TLS1_0",
  "name": "dineshstorage4321",
  "networkRuleSet": {
    "bypass": "AzureServices",
    "defaultAction": "Allow",
    "ipRules": [],
    "ipv6Rules": [],
    "resourceAccessRules": null,
    "virtualNetworkRules": []
  },
  "primaryEndpoints": {
    "blob": "https://dineshstorage4321.blob.core.windows.net/",
    "dfs": "https://dineshstorage4321.dfs.core.windows.net/",
    "file": "https://dineshstorage4321.file.core.windows.net/",
    "internetEndpoints": null,
    "microsoftEndpoints": null,
    "queue": "https://dineshstorage4321.queue.core.windows.net/",
    "table": "https://dineshstorage4321.table.core.windows.net/",
    "web": "https://dineshstorage4321.z13.web.core.windows.net/"
  },
  "primaryLocation": "eastus",
  "privateEndpointConnections": [],
  "provisioningState": "Succeeded",
  "publicNetworkAccess": null,
  "resourceGroup": "dineshapirgnew",
  "routingPreference": null,
  "sasPolicy": null,
  "secondaryEndpoints": null,
  "secondaryLocation": null,
  "sku": {
    "name": "Standard_LRS",
    "tier": "Standard"
  },
  "statusOfPrimary": "available",
  "statusOfSecondary": null,
  "storageAccountSkuConversionStatus": null,
  "tags": {},
  "type": "Microsoft.Storage/storageAccounts"
}
```
**Using Azure Powershell:**

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
### Create Azure Containers within Storage Account --

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
