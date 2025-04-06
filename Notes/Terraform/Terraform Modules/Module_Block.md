



```
az group create -l centralindia -n dkc-state-rg
az storage account create --name dkcstatestrgacct01 --resource-group dkc-state-rg --location centralindia --sku Standard_LRS
az storage container create --account-name dkcstatestrgacct01 --name mystate0190
```



