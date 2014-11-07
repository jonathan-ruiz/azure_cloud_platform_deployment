# Creating a linux based cloud platform in azure from Linux
** azure-cli version 8.11**

## Downloding credentials from Azure
    
    azure account download
## Importing credentials 

    azure account import publishsettings.publishsettings
## Adding an affinity group
If you don't create an affinity group before to try other commands you'll have errors like "parameter.label cannot be empty" what is very confusing.

    azure account affinity-group create affinity-group-name --label affinity-group-label  --location "West Europe"

## Adding a cloud service
    
    azure service create --serviceName {{ azure_cloud_service_name }} --description "{{ azure_cloud_service_description }}" --affinitygroup {{ azure_affinity_group_name }}
## Adding a storage account

    azure storage account create --description "Storage account description" --location "West Europe" --disable-geoReplication storageAccountName
## Adding a virtual network 
**Tested and not working in version 0.8.11** 

    azure network vnet create virtual-network-name --location "West Europe"
## Adding a virtual machine into the cloud service
### Using parameters
**Tested and not working in version 0.8.11** 

    azure vm create cloud-service OS_image admin_user --availability-set availability_set --vm-name virtual_machine_name --ssh 22 --no-ssh-password --ssh-cert ~/.ssh/id_rsa.pub.pem --vm-size Large

### Using a json file to create a new virtual machine
**Tested and not working in version 0.8.11 (rule.oreder index issue)** 

## Adding virtual machine endpoints

## Adding adding endpoints ACL rules
