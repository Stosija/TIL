## How to access a key vault during a terraform deployment

While working on a project we ran into the issue of how to keep our passwords secret during the Terraform deployment. [This article](https://blog.azureandbeyond.com/2019/01/24/how-to-securely-deploy-azure-infrastructures/) gave a great overview of how to make your Terraform deployment secure. The way to access keys is by putting this in the template file:

```
data "azurerm_key_vault_secret" "mySecret" {
name = "mySecretName"
vault_uri = "https://myKeyVaultName.vault.azure.net/"
}
```
It can then be referenced whenever you need it, ex:

```
resource "azure_virtual_machinge" "myAzureVM" {
os_profile {
computer_name = "myvm"
admin_username= "labuser"
admin_password= "${data.azurerm_key_vault_secret.mySecret.value}"
}
}
```
