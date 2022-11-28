# Quarkus CoffeeShop  demo on the Edge Management console
> Contributions are welcome.
Deploy the Quarkus CoffeeShop demo on the Edge Management console using Ansible Automation Platform.

![20221125111926](https://i.imgur.com/vmEIc7S.jpg)
---
![20221125124747](https://i.imgur.com/ilGr1YE.png)
---
![20221125124818](https://i.imgur.com/uOCOzmV.png)

## Prerequisites
* Ansible Automation Platform 
* Add Credentials to target machine 
* Build image job 
* Download ISO job 
* Deploy to KVM job


## Ensure Target Machine is created 
> Give privilege access to the target machine to the Ansible Automation Platform user.
![20221121095704](https://i.imgur.com/d2OLzqK.png)
![20221121095902](https://i.imgur.com/hFbPiui.png)
## Build Image Job Parameters
Add the following Job Tags for image builds:
* get_build_status
* build_image
```yaml
---
#########################################################
## Directories
### For Tower 
## for workstation: iso_download_directory: "/opt/generated_iso"
iso_download_directory: "/opt/generated_iso"

### For Tower 
## for workstation: workspace: "/opt/lib/aws/projects/workspace"
workspace: "/opt/workspace"

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

**RHEL Username**
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


## Auto register Quarkus CoffeeShop demo on the Edge Management console 

### Job Parameters
Add the following Job Tags for image builds:
* download_latest_iso
* configure_auto_registration
```yaml
---
#########################################################
## Directories
### For Tower 
## for workstation: iso_download_directory: "/opt/generated_iso"
iso_download_directory: "/opt/generated_iso"

### For Tower 
## for workstation: workspace: "/opt/lib/aws/projects/workspace"
workspace: "/opt/workspace"

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

## KVM VM deployment 
libvirt_iso_name: "{{ image_name }}_fleet_out.iso"
libvirt_vm_name:  rhel-edge-kvm
libvirt_image_dir: /var/lib/libvirt/images
libvirt_iso_dir:  /var/lib/libvirt/images
template_dir: "{{ iso_download_directory }}"
libvirt_defaults:
  edge_device:
    cpu: 4
    memory: 8388608

virtual_machines:
  - name: "{{ libvirt_vm_name }}"
    hostname: "{{ libvirt_vm_name }}" # there is a character limit with the hostname it will brake sysprep
    password: "{{ libvirt_vm_name }}"
    os: "rhel85"
    isos:
      - name: "{{ libvirt_iso_name }}"
        dev: sdb
    disk_size: 20G
    image_index: 2
    image_name: "RHEL Edge image"
    disk_iso: "{{ libvirt_vm_name }}"
    connection_type: "network" # "bridge" or "network" bridge is default
    bridgename: "default" 
    bridge_mac: "{{ '52:54:00' | community.general.random_mac }}"
    vlanid: 0 # use 503 in network mode for emulated lab or 0 in hardware bridge mode
    subnet: "192.168.122.1/24"
    secondary_dns: 1.1.1.1

```

### Survey Variables

**RHEL Username**
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


## Deploy Quarkus CoffeeShop demo vm on KVM

### Job Parameters
Add the following Job Tags for image builds:
* create_kvm_vm
```yaml
---
#########################################################
## Directories
### For Tower 
## for workstation: iso_download_directory: "/opt/generated_iso"
iso_download_directory: "/opt/generated_iso"

### For Tower 
## for workstation: workspace: "/opt/lib/aws/projects/workspace"
workspace: "/opt/workspace"

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

## KVM VM deployment 
libvirt_iso_name: "{{ image_name }}_fleet_out.iso"
libvirt_vm_name:  rhel-edge-kvm
libvirt_image_dir: /var/lib/libvirt/images
libvirt_iso_dir:  /var/lib/libvirt/images
template_dir: "{{ iso_download_directory }}"
libvirt_defaults:
  edge_device:
    cpu: 4
    memory: 8388608

virtual_machines:
  - name: "{{ libvirt_vm_name }}"
    hostname: "{{ libvirt_vm_name }}" # there is a character limit with the hostname it will brake sysprep
    password: "{{ libvirt_vm_name }}"
    os: "rhel85"
    isos:
      - name: "{{ libvirt_iso_name }}"
        dev: sdb
    disk_size: 20G
    image_index: 2
    image_name: "RHEL Edge image"
    disk_iso: "{{ libvirt_vm_name }}"
    connection_type: "network" # "bridge" or "network" bridge is default
    bridgename: "default" 
    bridge_mac: "{{ '52:54:00' | community.general.random_mac }}"
    vlanid: 0 # use 503 in network mode for emulated lab or 0 in hardware bridge mode
    subnet: "192.168.122.1/24"
    secondary_dns: 1.1.1.1

```

### Survey Variables

**RHEL Username**
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

