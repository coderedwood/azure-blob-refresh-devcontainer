# azure_blob_refresh_devcontainer
## Commands
```
az login
```
```
az group create --location eastus2 --name az204-storageblobs-rg24
```
```
az storage account create --location eastus2 --name az204blobaccount24 --resource-group az204-storageblobs-rg24 --sku Standard_RAGRS --kind BlobStorage --access-tier Hot
```
```
az storage account keys list --name az204blobaccount24 --resource-group az204-storageblobs-rg24 --output table
```
### Copy the output and make note of the keys

```
az storage container create --name az204blobcontainer --account-name az204blobaccount24 --account-key <<place account one of the account keys from output>>
```
```
echo "random blob text for azure blobs exercise" > azblobtext.txt
```
uze the azure portal to add a "Storage blob Owner" permissions via the "Access Control(IAM)" to the storage account
```
az storage blob upload --account-name az204blobaccount24 --container-name az204blobcontainer --file "azblobtext.txt" --name azblobtext.txt --auth-mode login --overwrite
```
### You can list the blobs in the blob container by running the commmand below
```
az storage blob list --account-name az204blobaccount24 --container-name az204blobcontainer --output table --auth-mode login
```
### You can also check to see if the container exists via the command below
```
az storage container exists --account-name az204blobaccount24 --auth-mode login --name az204blobcontainer
```
### Delete the blob/file using the command below.

```
az storage blob delete --account-name az204blobaccount24 --container-name az204blobcontainer --name azblobtext.txt --auth-mode login
```
### Delete the resource group when finished to avoid any charges.

```
az group delete --name az204-storageblobs-rg24 --no-wait -y
```