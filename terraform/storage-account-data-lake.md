## How to create a storage account for Azure Data Lake Storage

I don't know much about how Data Lakes work yet, so it took me a minute to realize how to properly configure a storage account for Data Lake Gen 2. You have to go into the Advanced settings tab and enable hierarchical naming. For Terraform the configuration will look like this:

```
resource "azurerm_storage_account" "example" {
  name                = "storageaccountname"
  resource_group_name = azurerm_resource_group.example.name
  location                 = azurerm_resource_group.example.location
  account_tier             = "Standard"
  account_replication_type = "LRS"
  is_hns_enabled           = "true"
  ```
  
  `is_hns_enabled` must be a lower case boolean value. This is kind of buried in the Terraform documentation.
