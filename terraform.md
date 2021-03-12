## Store Remote State

Configure Storage Account

* **storage_account_name: The name of the Azure Storage account.**
* **container_name: The name of the blob container.**
* **key: The name of the state store file to be created.**
* **access_key: The storage access key.**

Create an environment variable named ARM_ACCESS_KEY with the value of the Azure Storage access key.

* **export ARM_ACCESS_KEY=<storage access key> or export ARM_ACCESS_KEY=$(az keyvault secret show --name terraform-backend-key --vault-name myKeyVault --query value -o tsv)**

```
terraform {
  backend "azurerm" {
    resource_group_name   = "*****"
    storage_account_name  = "******"
    container_name        = "*****"
    key                   = "********"
  }
}
```
