# Using RedHat Redfish Ansible collection and HPE iLO collection

Examples of playbooks 

## Pre-requisites
 - RHEL OS - current release
 - Python3 - current release
 - Ansible - current release
 - Redfish python library installed: pip3 install redfish==3.0.2
 - Redfish collection from RedHat community: ansible-galaxy collection install community.general
 - HPE iLO collection from RedHat: ansible-galaxy collection install hpe.ilo

 - Target servers: 
   - iLO firmware > 2.65
   - [PLDM RDE](https://developer.hpe.com/blog/overview-of-the-platform-level-data-model-for-redfish%C2%AE-device-enablement-standard/) Storage controllers(SR, MR, NS controllers) firmware: 5.00  

## Environment Variables
 - export ANSIBLE_LIBRARY=/location-where-ansible-collections-are-installed/hpe/ilo/plugins/modules
 - export ANSIBLE_MODULE_UTILS=/location-where-ansible-collections-are-installed/hpe/ilo/plugins/module_utils

## Example 1 - Querying iLO
 This set of playbooks will query iLO servers to collect data exposed with Redfish and generate CSV / JSON files

### CSV input file
  The CSV file contains list of IP addresses and iLO credentials of target servers. The format is:
  ilo_ip, ilo_username,ilo_password,site

### System Inventory Playbooks

        - system-inventory.yml  --> system-inventory-tasks.yml    --> system-sub-inventory-cpu.yml, system-sub-inventory-firmware.yml
        - memory-inventory.yml  --> memory-inventory-tasks.yml    --> memory-sub-inventory.yml
        - nic-inventory.yml     --> nic-inventory-tasks.yml       --> nic-manager-sub-inventory.yml, nic-sub-inventory.yml
        - storage-inventory.yml --> storage-inventory-tasks.yml   --> storage-sub-inventory-controller.yml, storage-sub-inventory-pdisk.yml,storage-sub-inventory-ldisk.yml
        - psu-inventory.yml     --> psu-inventory-tasks.yml       --> psu-sub-inventory.yml

### Commands to run
        - ansible-playbook system-inventory.yml --extra-vars "server_csv=list-servers.csv"
        - ansible-playbook memory-inventory.yml --extra-vars "server_csv=list-servers.csv"
        - ansible-playbook nic-inventory.yml --extra-vars "server_csv=list-servers.csv"
        - ansible-playbook storage-inventory.yml --extra-vars "server_csv=list-servers.csv"
        - ansible-playbook psu-inventory.yml --extra-vars "server_csv=list-servers.csv"

        - 1.3 Playbooks
    



  
