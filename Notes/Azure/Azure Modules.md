## Azure Resource Group Creation

**Objective:** This assignment will help you understand how to create an Azure Resource Group using both the Azure Portal and Azure CLI. By the end of this exercise, you should be comfortable working with Azure Resource Groups through different methods.

### **Part 1:** Login to Azure Portal
Open your web browser and go to Azure Portal.
Use the credentials provided by your Group Leads to sign in.
Ensure that you have the necessary permissions to create resources.

### **Part 2:** Create a Resource Group Using Azure Portal
In the Azure Portal, search for Resource Groups in the top search bar and select it.
Click on the + Create button to create a new Resource Group.
Fill in the required details:
Subscription: Select the appropriate subscription.
Resource Group Name: Choose a unique name for your Resource Group.
Region: Select the region closest to your users or application needs.
Explore and read about all the available options while creating the Resource Group.
Click Review + Create and then Create to deploy the Resource Group.
Verify the successful creation of the Resource Group by navigating back to the Resource Groups section.

### Part 3: Create a Resource Group Using Azure CLI & Azure Powershell:

### i. Azure CLI Module --
Install Azure CLI and Create a Resource Group Using CLI
Install Azure CLI:
we can download and install Azure CLI with different methods:
a) Microsoft Installer (MSI)
b) WinGet (Windows Package Manager)
c) Microsoft Installer (MSI) with PowerShell
d) ZIP Package

Download and install the Azure CLI from Azure CLI Installation Guide.
Verify installation by running the following command in the terminal:
```powershell
az --version
```
Login to Azure using CLI:

Open a terminal or command prompt and run:
```powershell
az login
```
A browser window will open asking you to log in to your Azure account. Use the credentials provided by your Group Leads.
After successful login, the CLI will display the list of available subscriptions.
Create a Resource Group using CLI:

#### Run the following command to create a new Resource Group named rg-cli:
```powershell
az group create --name RG-DKC --location centralindia
```
Replace eastus with your preferred region if needed.

#### Verify the creation by running:
```powershell
az group list --output table   or    az group list -o table
```
#### Delete a Resource Group --
```powershell
az group delete -n RG-DKC
```
#### Create VM Using Azure CLI --
```powershell
az vm create -n MyWinVm -g RG-DKC --public-ip-address "" --image Win2019Datacenter
```
#### Delete VM Using Azure CLI --
```powershell
az vm delete -g RG-DKC -n MyWinVm
```

### ii. Azure PowerShell Module --

We are Installing Azure PowerShell Module with two different methods:
a) The MSI package for Azure PowerShell
b) PowerShell Gallery

Azure PowerShell can be installed via PowerShell Gallery. Follow these steps:

#### 1. Install PowerShell (if not already installed) --

Ensure you have PowerShell 7 or later installed. You can check the version using:
```powershell
$PSVersionTable.PSVersion
```
#### 2. Install Azure PowerShell Module --

To install the latest version of the Az module, open PowerShell as Administrator and run:
```powershell
Install-Module -Name Az -AllowClobber -Scope AllUsers -Force
```
Note: The -AllowClobber flag ensures that any existing conflicting modules are overridden.

#### 3. Verify Installation --

Check if Azure PowerShell is installed successfully:
```powershell
Get-Module -ListAvailable -Name Az*
```
#### Logging in to Azure --

Once the module is installed, log in to your Azure account using the following command:
```powershell
Connect-AzAccount
```
This will prompt a browser-based authentication. After successful login, the active subscription details will be displayed.

#### Selecting a Specific Subscription --

If you have multiple subscriptions, list them using:
```powershell
Get-AzSubscription
```
To select a specific subscription, use:
```powershell
Set-AzContext -SubscriptionId <your-subscription-id>
```
#### Creating a Resource Group using Azure Powershell --
A resource group is a logical container for Azure resources. To create one, use the following command:
```powershell
New-AzResourceGroup -Name "RG-DKC" -Location "CentralIndia"
```
Replace myResourceGroup with your preferred name and EastUS with the desired Azure region.

#### Confirm the Resource Group Creation --

To verify that the resource group was created successfully, use:
```powershell
Get-AzResourceGroup -Name "RG-DKC"
```
#### Quickstart: Create a Windows virtual machine in Azure with PowerShell --
```powershell
New-AzVm -ResourceGroupName 'RG-DKC' -Name 'MotaVM1' -Location 'centralindia' -Image 'MicrosoftWindowsServer:WindowsServer:2022-datacenter-azure-edition:latest' -VirtualNetworkName 'myVnet1' -SubnetName 'mySubnet1' -SecurityGroupName 'myNSG1' -PublicIpAddressName 'myPublicIpAddress1' -OpenPorts 80,3389
```
#### Deleting a Resource Group (If Needed) --
```powershell
Remove-AzResourceGroup -Name "RG-DKC" -Force
```
#### See List in table form --

az group list -o table

az account list -o table

az resource list -o table

### iii. Rest API --
#### Resource group created by RestApi/POSTMAN:
Prerequisites: Download Postman - https://www.postman.com/downloads/

**1.**	CLI/Power shell login and find the subscription id.
**Example-**
```powershell
az account list --output table
```
```powershell
f85ee25f-ffbe-4145-896a-4a245999982e
```
**2.	Postman**
Put https://management.azure.com/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups<resourcegroupname>?api-version=2024-11-01

Example: https://management.azure.com/subscriptions/f85ee25f-ffbe-4145-896a-4a245999982e/resourceGroups/dineshapirg?api-version=2024-11-01
**3.	Params** 
api-version       2024-11-01
 
**4.	Authorization**
Type ---Bearer Token| <Token>
Find Token: az account get-access-token --query accessToken --output tsv
**Example:** eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImltaTBZMnowZFlLeEJ0dEFxS19UdDVoWUJUayIsImtpZCI6ImltaTBZMnowZFlLeEJ0dEFxS19UdDVoWUJUayJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuY29yZS53aW5kb3dzLm5ldC8iLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8xNmI4MDUzNC0wOTdjLTRiNWEtOWZhYi1mN2NiMzE4NTgxNjAvIiwiaWF0IjoxNzQwMDMwODQyLCJuYmYiOjE3NDAwMzA4NDIsImV4cCI6MTc0MDAzNTY0NiwiYWNyIjoiMSIsImFpbyI6IkFWUUFxLzhaQUFBQTNOSU1xLzg1V1lOeWxDbXl5aDdTRVdxWXlZTzlnZVNsaU83enVJNm9mT0VIcmhqVDZpV1F0NHVITWdDOWJyUXFpak0zaWJTcllUclNLLzRYb0V1NllSV05hK0lYZFhhWjV0bHM0dWhHQ1ZzPSIsImFtciI6WyJwd2QiLCJtZmEiXSwiYXBwaWQiOiIwNGIwNzc5NS04ZGRiLTQ2MWEtYmJlZS0wMmY5ZTFiZjdiNDYiLCJhcHBpZGFjciI6IjAiLCJncm91cHMiOlsiNzY4NTg5ZGItYTFmOC00M2QwLTk2OTgtODU1MWQzNDBkMTg3Il0sImlkdHlwIjoidXNlciIsImlwYWRkciI6IjYxLjk1LjE5OS4xMzgiLCJuYW1lIjoiRGluZXNoIEt1bWFyIiwib2lkIjoiYWZkNDUxYzAtM2EyMi00ZjQxLTk2ZjQtOTRmODc4NzRkNGZiIiwicHVpZCI6IjEwMDMyMDA0NDlGNjkyREUiLCJwd2RfdXJsIjoiaHR0cHM6Ly9wb3J0YWwubWljcm9zb2Z0b25saW5lLmNvbS9DaGFuZ2VQYXNzd29yZC5hc3B4IiwicmgiOiIxLkFjWUFOQVc0Rm53SldrdWZxX2ZMTVlXQllFWklmM2tBdXRkUHVrUGF3ZmoyTUJQR0FNckdBQS4iLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzaWQiOiIwMDIxOTlhOS05ODNjLTliOGQtNjVlMy02MzdhMTk0YzA1NjQiLCJzdWIiOiJTM3RsQ25OZDdoaDg2S0lxUkpFQ0VKLWVVMVljTlpYQnozc3pKRGtBZkNFIiwidGlkIjoiMTZiODA1MzQtMDk3Yy00YjVhLTlmYWItZjdjYjMxODU4MTYwIiwidW5pcXVlX25hbWUiOiJEaW5lc2hAcm9oaXRrYXVyYXYyNWdtYWlsLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6IkRpbmVzaEByb2hpdGthdXJhdjI1Z21haWwub25taWNyb3NvZnQuY29tIiwidXRpIjoiRVFjMEhLa2N6a1d3VEhqajJma1lBQSIsInZlciI6IjEuMCIsIndpZHMiOlsiYjc5ZmJmNGQtM2VmOS00Njg5LTgxNDMtNzZiMTk0ZTg1NTA5Il0sInhtc19jYWUiOiIxIiwieG1zX2NjIjpbIkNQMSJdLCJ4bXNfZmlsdGVyX2luZGV4IjpbIjE5OCJdLCJ4bXNfaWRyZWwiOiIxIDQiLCJ4bXNfcmQiOiIwLjQyTGpZQlJpT3NZSUFBIiwieG1zX3NzbSI6IjEiLCJ4bXNfdGNkdCI6MTczOTI5MjA4NH0.FEtZVPPeyMC8QRG34UMFuVNKZ0oPi1RpKWMgEUyC4k0--gb4VH70n3pgx-7jW7njYmTzjtTnmCt3Hr5pLaR1MwCitTkhD1wkReB51q4plOE6zxkm00LKkdwxXkg-U_YgCkw5e8v08l4-FqajqhjJEjUV-JKREC6IveG6WSZwbAykdu93IodLysVH3l2zy0mat9NzKUvdj4mSh7Ci-ulYFEMwq08tNLSrge39aARk_lo_flpkn8ZBFqjKn-_xyLDSMojUpA9X2cs2V16BGPjqNrS0a-FRxvFZytQYXnf7WBBCyXVSn6uiHV8mvkdwlHvyrLZUzFZ2uUUQ38OeJNi7RA 
 
**5.	Headers**
Authorization              Bearer <token>
Content-Type              application/json

**6.	body** 
{
    "location": "eastus",
    "tags": {
        "environment": "developer",
        "owner":  "dineshapirg"
    }
}

 
**7.	Result -**
 
Go to Azure Portal and check Resource Group 

What is Postman?
Postman is a powerful API development tool that helps developers test, debug, and document APIs effortlessly.
It's widely used for sending API requests, automating tests, and collaborating on API development.
Think of it as a browser for APIs, where you can send requests (GET, POST, PUT, DELETE) and see responses without writing a single line of code.

Working with APIs
🔹 Authorization – Set API keys, OAuth, or Bearer Tokens
🔹 Headers & Body – Add request headers & JSON body











