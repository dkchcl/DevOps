Configuring Azure CLI authentication in Terraform
Now that we're logged into the Azure CLI - we can configure Terraform to use these credentials.
```
Note:
In version 4.0 of the Azure Provider, it's now required to specify the Azure Subscription ID when configuring a provider instance in your configuration. This can be done by specifying the subscription_id provider property, or by exporting the ARM_SUBSCRIPTION_ID environment variable. More information can be found in the Azure Resource Manager: 4.0 Upgrade Guide.
```
