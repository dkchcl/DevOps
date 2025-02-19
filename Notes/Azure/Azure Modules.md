## Azure Resource Group Creation

#### Objective: This assignment will help you understand how to create an Azure Resource Group using both the Azure Portal and Azure CLI. By the end of this exercise, you should be comfortable working with Azure Resource Groups through different methods.

Part 1: Login to Azure Portal
Open your web browser and go to Azure Portal.
Use the credentials provided by your Group Leads to sign in.
Ensure that you have the necessary permissions to create resources.

Part 2: Create a Resource Group Using Azure Portal
In the Azure Portal, search for Resource Groups in the top search bar and select it.
Click on the + Create button to create a new Resource Group.
Fill in the required details:
Subscription: Select the appropriate subscription.
Resource Group Name: Choose a unique name for your Resource Group.
Region: Select the region closest to your users or application needs.
Explore and read about all the available options while creating the Resource Group.
Click Review + Create and then Create to deploy the Resource Group.
Verify the successful creation of the Resource Group by navigating back to the Resource Groups section.

## Part 3: Create a Resource Group Using Azure CLI & Azure Powershell

### i. Azure CLI Module --
Install Azure CLI and Create a Resource Group Using CLI
Install Azure CLI:
we can download and install Azure CLI in different methods:
a) Microsoft Installer (MSI)
b) WinGet (Windows Package Manager)
c) Microsoft Installer (MSI) with PowerShell
d) ZIP Package

Download and install the Azure CLI from Azure CLI Installation Guide.
Verify installation by running the following command in the terminal:

az --version

Login to Azure using CLI:

Open a terminal or command prompt and run:

az login

A browser window will open asking you to log in to your Azure account. Use the credentials provided by your Group Leads.
After successful login, the CLI will display the list of available subscriptions.
Create a Resource Group using CLI:

Run the following command to create a new Resource Group named rg-cli:

az group create --name RG-DKC --location centralindia

Replace eastus with your preferred region if needed.
Verify the creation by running:

az group list --output table   or    az group list -o table

#### Delete a Resource Group --

az group delete -n RG-DKC

#### Create VM Using Azure CLI --

az vm create -n MyWinVm -g RG-DKC --public-ip-address "" --image Win2019Datacenter

#### Delete VM Using Azure CLI --

az vm delete -g RG-DKC -n MyWinVm


### ii. Azure PowerShell Module --

Installing Azure PowerShell Module

Azure PowerShell can be installed via PowerShell Gallery. Follow these steps:

### 1. Install PowerShell (if not already installed) --

Ensure you have PowerShell 7 or later installed. You can check the version using:

$PSVersionTable.PSVersion

### 2. Install Azure PowerShell Module --

To install the latest version of the Az module, open PowerShell as Administrator and run:

Install-Module -Name Az -AllowClobber -Scope AllUsers -Force

Note: The -AllowClobber flag ensures that any existing conflicting modules are overridden.

### 3. Verify Installation --

Check if Azure PowerShell is installed successfully:

Get-Module -ListAvailable -Name Az*

### Logging in to Azure --

Once the module is installed, log in to your Azure account using the following command:

Connect-AzAccount

This will prompt a browser-based authentication. After successful login, the active subscription details will be displayed.

### Selecting a Specific Subscription --

If you have multiple subscriptions, list them using:

Get-AzSubscription

To select a specific subscription, use:

Set-AzContext -SubscriptionId <your-subscription-id>

### Creating a Resource Group using Azure Powershell --
A resource group is a logical container for Azure resources. To create one, use the following command:

New-AzResourceGroup -Name "RG-DKC" -Location "CentralIndia"

Replace myResourceGroup with your preferred name and EastUS with the desired Azure region.

### Confirm the Resource Group Creation --

To verify that the resource group was created successfully, use:

Get-AzResourceGroup -Name "RG-DKC"

### Quickstart: Create a Windows virtual machine in Azure with PowerShell --

New-AzVm -ResourceGroupName 'RG-DKC' -Name 'MotaVM1' -Location 'centralindia' -Image 'MicrosoftWindowsServer:WindowsServer:2022-datacenter-azure-edition:latest' -VirtualNetworkName 'myVnet1' -SubnetName 'mySubnet1' -SecurityGroupName 'myNSG1' -PublicIpAddressName 'myPublicIpAddress1' -OpenPorts 80,3389

### Deleting a Resource Group (If Needed) --

Remove-AzResourceGroup -Name "RG-DKC" -Force

### See List in table form---------------

az group list -o table

az account list -o table

az resource list -o table















