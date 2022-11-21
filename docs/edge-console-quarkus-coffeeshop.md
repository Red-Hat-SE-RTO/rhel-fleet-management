# Quarkus CoffeeShop  demo on the Edge Management console  - WIP
> Contributions are welcome current work in progress currently building. 
Deploy the Quarkus CoffeeShop demo on the Edge Management console using Ansible Automation Platform.

## Prerequisites
* Ansible Automation Platform 
* Add Credentials to target machine 
* Build image job 
* Download ISO job 
* Deploy to KVM job
* [Create a custom repository](https://github.com/redhat-et/microshift-demos/tree/main/demos/edge-console-demo#create-a-custom-repository)

## Ensure Target Machine is created 
> Give privilege access to the target machine to the Ansible Automation Platform user.
![20221121095704](https://i.imgur.com/d2OLzqK.png)
![20221121095902](https://i.imgur.com/hFbPiui.png)
## Build Image Job Parameters
Add 
The following Job Tags for image builds:
* get_build_status
* build_image
```
---
#########################################################
## Direcoties
### For Tower 
## for workstation: iso_download_directory: "/opt/generated_iso"
iso_download_directory: "/tmp/generated_iso"

### For Tower 
## for workstation: workspace: "/opt/lib/aws/projects/workspace"
workspace: "/tmp"

#########################################################
## Required Files
ssh_pub_key: "CHANGEME"

#########################################################
## required variables
create_device_name_group: true
device_group_name: "my-device-name-group"
create_image: true

#########################################################
## image atrributes
image_name: "quarkuscoffeeshop-majestic-monolith-11-21-2022-b1" # Example: "test-image-11-13-2022-b1"
username: "admin"
distribution: "rhel-86"
description: "sample description"
build_template: image-build # for microshift deployments use image-mircoshift-build
mircroshift_deployment: false
arch: "x86_64"
kickstart_path: "https://raw.githubusercontent.com/Red-Hat-SE-RTO/rhel-fleet-management/main/inventories/lab/applications/quarkuscoffeeshop-majestic-monolith-fleet-manger/fleet_kspost.txt"

#########################################################
## automated management variables
## https://access.redhat.com/management/activation_keys
rhc_org_id: "1111111"
rhc_activation_key: "CHANGEME"

#########################################################
## optional variables
## osinfo-query os
os_variant: "rhel8.6"

#########################################################
## Dont need to change 
compiled_uri_headers: {}
```
### Survey Variables

**RHEL Username **
* Required: true  
* Question:`RH Username:` . 
* Type: Text
* Answer variable name: `rh_authentication_basic_username` . 

**RHEL Password**
* Required: true   
* Question: `RH Password:` . 
* Type: Password
* Answer variable name: `rh_authentication_basic_password` . 


**API Token:**
> [Red Hat API Tokens](https://access.redhat.com/management/api) . 
* Required: true  
* Question: `RH Token:` . 
* Type: Password
* Answer variable name: `rh_offline_authentication_api_bearer_token` . 

![20221121102135](https://i.imgur.com/YOvbg97.png)