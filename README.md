
# 準備

vscode
HashiCorp Terraform 拡張

## install terraform 
```
brew install tfenv
tfenv --version
tfenv list-remote
```
```
tfenv install 1.1.4
tfenv use 1.1.4
```

```
% terraform -v 
Terraform v1.1.4
on darwin_amd64
```

# az login

## remote state 格納先
```
#!/bin/bash

RESOURCE_GROUP_NAME=my-tfstate-rg
STORAGE_ACCOUNT_NAME=tfstate$RANDOM
CONTAINER_NAME=tfstate

# Create resource group
az group create --name $RESOURCE_GROUP_NAME --location japaneast

# Create storage account
az storage account create --resource-group $RESOURCE_GROUP_NAME --name $STORAGE_ACCOUNT_NAME --sku Standard_LRS --encryption-services blob

# Create blob container
az storage container create --name $CONTAINER_NAME --account-name $STORAGE_ACCOUNT_NAME
```

```
ACCOUNT_KEY=$(az storage account keys list --resource-group $RESOURCE_GROUP_NAME --account-name $STORAGE_ACCOUNT_NAME --query '[0].value' -o tsv)
export ARM_ACCESS_KEY=$ACCOUNT_KEY
```
