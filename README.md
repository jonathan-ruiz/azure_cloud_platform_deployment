# Creating a Linux based cloud platform in azure from Linux with azure Linux tools
** azure-cli version 8.11**

## Downloding credentials from Azure
    
    azure account download
## Importing credentials 

    azure account import publishsettings.publishsettings
## Adding an affinity group
If you don't create an affinity group before to try other commands you'll have errors like "parameter.label cannot be empty" what is very confusing.
    
    azure account affinity-group create {{ azure_affinity_group_name }} --label {{ azure_affinity_group_name }}  --location "{{ azure_affinity_group_location }}"
    
## Adding a cloud service
    
    azure service create --serviceName {{ azure_cloud_service_name }} --description "{{ azure_cloud_service_description }}" --affinitygroup {{ azure_affinity_group_name }}
    
## Adding a storage account

    azure storage account create --description "{{ azure_storage_account_description }}" --affinity-group {{ azure_affinity_group_name }} --disable-geoReplication {{ azure_storage_account_name }} --disable-geoReplication storageAccountName
    
## Adding a virtual network 
**Tested and not working in version 0.8.11** 

    azure network vnet create {{ azure_virtual_network_name }} --affinity-group {{ azure_affinity_group_name }}
    
## Export Virtual machine configuration

    azure vm export {{ azure_virtual_machine_name }} {{ json_file_path }}

## Adding a virtual machine into the cloud service

### Using parameters
    
    azure vm create {{ azure_cloud_service_name }} {{ azure_virtual_machine_image }} {{ azure_virtual_machine_user }} --availability-set {{ azure_virtual_machine_availabolity_set }} --vm-name {{ azure_virtual_machine_base_name }}{{ item }} --ssh {{ azure_virtual_machine_ssh_port }} --no-ssh-password --ssh-cert {{ azure_virtual_machine_user_public_key_path }} --vm-size {{ azure_virtual_machine_size }}

### Using a json file to create a new virtual machine
**Tested and not working in version 0.8.11 (https://github.com/Azure/azure-sdk-for-node/issues/1335)** 

## Adding virtual machine endpoints

    azure vm endpoint create {{ azure_virtual_machine_name }} {{ public_port }} {{ private_port }}

## Adding endpoints ACL rules
    ** Not found - Alternatively use 'vm create-from' command **

## Other useful commands
### Copy files between storage accounts

    azure storage container sas create -a {{ azure_storage_account_name }} -k {{ azure_storage_account_management_key }} {{ azure_storage_container_name}} {{ azure_storage_premisions }} {{ azure_storage_expiry }}
    azure storage blob copy start -a {{ azure_strage_destination_account_name }} -k {{ azure_strage_destination_account_management_key }} {{ azure_source_uri}}?{{ azure_previous_step_generated_shared_access_signatured }} {{ azure_destination_container}}
### Create a storage file share

    azure storage share create -a {{azure_storage_account_name}} -k {{ azure_storage_account_key }} {{ azure_storage_file_share_name }} ** NEED ACCESS TO FILE SHARE SERVICE **
