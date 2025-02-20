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

1.	CLI/Power shell login and find the subscription id
**Example-**
```powershell
az account list --output table
```
f85ee25f-ffbe-4145-896a-4a245999982e

3.	Postman
Put https://management.azure.com/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups<resourcegroupname>?api-version=2021-10-01

Example: https://management.azure.com/subscriptions/f85ee25f-ffbe-4145-896a-4a245999982e/resourceGroups/dineshapirg?api-version=2021-10-01
3.	Params 
api-version       2021-10-01
 
4.	Authorization
Type ---Bearer Token| <Token>
Find Token: az account get-access-token --query accessToken --output tsv
Example: eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImltaTBZMnowZFlLeEJ0dEFxS19UdDVoWUJUayIsImtpZCI6ImltaTBZMnowZFlLeEJ0dEFxS19UdDVoWUJUayJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuY29yZS53aW5kb3dzLm5ldC8iLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC9hZWQyYzQ3ZC1jYjM0LTRlMjgtYmU2OS0yOGJhNTc1ZjNkMGEvIiwiaWF0IjoxNzM5ODMyMTU0LCJuYmYiOjE3Mzk4MzIxNTQsImV4cCI6MTczOTgzNzE1MiwiYWNyIjoiMSIsImFpbyI6IkFXUUFtLzhaQUFBQWFQMVJqVngvTjUvWEx1ZHFhK296eXRVTGJYMlUxaDJKYXgxNE8vZlJvOUx1a25GaU5QK2dlNGdBMjkvcDc4WlFJdkE1bnA2cVVmTytSQzVHbDhldGJVcTFqQk5uaGNXaFFhZGVjNTJYeFYwaGc4cUdmVXdxQ2dYNWNmeDd5V3hXIiwiYWx0c2VjaWQiOiIxOmxpdmUuY29tOjAwMDNCRkZFOTA4OTg3MjQiLCJhbXIiOlsicHdkIl0sImFwcGlkIjoiMDRiMDc3OTUtOGRkYi00NjFhLWJiZWUtMDJmOWUxYmY3YjQ2IiwiYXBwaWRhY3IiOiIwIiwiZW1haWwiOiJjbG91ZC5zYW5qYXlzaW5naEBnbWFpbC5jb20iLCJmYW1pbHlfbmFtZSI6IlNpbmdoIiwiZ2l2ZW5fbmFtZSI6IlNhbmpheSIsImdyb3VwcyI6WyJlNDQ1YTE3MS03NjVkLTQxMWYtYmQyZi02YWI5Y2UwZmQ1NTIiXSwiaWRwIjoibGl2ZS5jb20iLCJpZHR5cCI6InVzZXIiLCJpcGFkZHIiOiIyNDAxOjQ5MDA6MWM2NjplMzVlOjFjMzA6NWVjYzo4ZDkxOjU5OGMiLCJuYW1lIjoiU2 
 
5.	Headers
Authorization              Bearer <token>
Content-Type              application/json

6.	body 
{
    "location": "eastus",
    "tags": {
        "environment": "developer",
        "owner":  "satyasin"
    }
}

 
7.	Result -
 
Go to Azure Portal and check Resource Group 

What is Postman?
Postman is a powerful API development tool that helps developers test, debug, and document APIs effortlessly.
It's widely used for sending API requests, automating tests, and collaborating on API development.
Think of it as a browser for APIs, where you can send requests (GET, POST, PUT, DELETE) and see responses without writing a single line of code.

Working with APIs
🔹 Authorization – Set API keys, OAuth, or Bearer Tokens
🔹 Headers & Body – Add request headers & JSON body











