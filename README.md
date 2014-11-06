# Creating a cloud platform in azure using "Azure Command-Line Tools for Mac and Linux"
## Adding a cloud service
    
    azure service create --serviceName cloud-service-name --description "cloud-service-name description" --location "West Europe"
## Adding a storage account

    azure storage account create --description "Storage account description" --location "West Europe" --disable-geoReplication storageAccountName
## Adding a virtual network 
**Tested and not working in version 0.8.11** 

    azure network vnet create virtual-network-name --location "West Europe"
## Adding a virtual machine

### Using a json file to create a new virtual machine
**Tested and not working in version 0.8.11 (rule.oreder index issue)** 

## Adding virtual machine endpoints

## Adding adding endpoints ACL rules
