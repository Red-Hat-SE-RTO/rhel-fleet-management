# RPM-DNF Image Builder Settings
With RPM-DNF, you can manage the system software by using the DNF package manager and updated RPM packages. This is a simple and adaptive method of managing and modifying the system over its lifecycle.

https://console.redhat.com/insights/image-builder

**Job Tags**
* get_insight_build_status
* rpm_dnf_build_image

**Job Variables**
```
---
#########################################################
## Directories
### For Tower 
## for workstation: iso_download_directory: "/opt/generated_iso"
iso_download_directory: "/tmp/generated_iso"
image_type: image-installer   # guest-image=qcow2 image-installer=iso

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
distribution: "rhel-92"
description: "sample description"
packages:  ["curl", "net-tools", "podman", "tar", "bind-utils", "git"]
# for osbuild tree  deployments image-build for microshift use image-microshift-build
# for rpm image builder use image-builder
build_template: image-builder
arch: "x86_64"
enable_kickstart: false 
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

**RHEL Username**
* Required: true  
* Question:`RH Username:` . 
* Answer variable name: `rhsm_username` . 
![20221113120730](https://i.imgur.com/Aze4OCN.png)

**RHEL Password**
* Required: true   
* Question: `RH Password:` . 
* Answer variable name: `rhsm_password` . 
![20221113120935](https://i.imgur.com/mjgWPBp.png)

**API Token:**
> [Red Hat API Tokens](https://access.redhat.com/management/api) . 
* Required: true  
* Question: `RH Token:` . 
* Answer variable name: `rh_offline_authentication_api_bearer_token` . 
![20221113121155](https://i.imgur.com/CnF4sqi.png)

![20221113121237](https://i.imgur.com/042j1mU.png)
