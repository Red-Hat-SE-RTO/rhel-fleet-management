# Download ISO from Fleet Manager


**Job Tags**
* get_build_status
* download_latest_iso
  
**Job Variables**
```
---
#########################################################
## Directories
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
image_name: "test-image" # Example: "test-image-11-13-2022-b1"
username: "admin"
distribution: "rhel-86"
description: "sample description"
packages: "curl net-tools podman tar bind-utils git"
arch: "x86_64"
mircroshift_deployment: false
kickstart_path: "https://raw.githubusercontent.com/Red-Hat-SE-RTO/rhel-fleet-management/main/inventories/lab/applications/quarkuscoffeeshop-majestic-monolith-fleet-manger/fleet.kspost"


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
* Answer variable name: `rh_authentication_basic_username` . 
![20221114093344](https://i.imgur.com/HyNlYqU.png)

**RHEL Password**
* Required: true   
* Question: `RH Password:` . 
* Answer variable name: `rh_authentication_basic_password` . 
![20221114093412](https://i.imgur.com/FMQaWkJ.png)

**API Token:**
> [Red Hat API Tokens](https://access.redhat.com/management/api) . 
* Required: true  
* Question: `RH Password:` . 
* Answer variable name: `rh_offline_authentication_api_bearer_token` . 
![20221114093458](https://i.imgur.com/ayCXAWR.png)

![20221114093201](https://i.imgur.com/pWqND5X.png)