# Get secret from Azure Key Vault using simple composite action

This action is designed to use the Azure CLI to get Azure Key Vault's secret values. It supports [Azure/login](https://github.com/Azure/login) using Azure credentials JSON. It also features optional autologout from Azure session.

# Usage

## Example
```
name: Get Key Vault's secret value

on:
  push:
    branches:
      - master

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v3
      - id: kv
        uses: DawidB/get-secret-from-keyvault@master
        with:
          azure_credentials: ${{ secrets.AZURE_CREDENTIALS }}
          key_vault_name: example-key-vault
          secret_name: example-connection-string
```

## Advanced scenario

Multiple secrets can be retrieved without lengthy multiple login-logout attempts. Just make a first action call with `azure_credentials` input and `auto_logout` set to `false`. Subsequent calls have to be made without `azure_credentials` provision and `auto_logout` value set to `false`. Final call should be left with default `auto_logout` value set to `true`.
          
## Input Variables

Input | Value | Required
---|---|:---:
azure_credentials | Credentials JSON with subscription id, tenant id, client id and client secret | No
key_vault_name | The name of the Azure Key Vault from which the secret value will be retrieved. |	Yes
secret_name	| Secret name. | Yes
auto_logout | Automatically log out of Azure session | No
