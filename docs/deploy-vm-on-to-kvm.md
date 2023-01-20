# Deploy KVM VM via Ansible Automation Platform 


**Job Tags**
* get_build_status
* configure_auto_registration
* download_latest_iso
* create_kvm_vm


**Job Variables**
```
---
#########################################################
## Directories
### For Tower 
## for workstation: iso_download_directory: "/opt/generated_iso"
iso_download_directory: "/tmp/"

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

#########################################################
## KVM VM deployment 
libvirt_iso_name: "{{ image_name }}.iso"
libvirt_vm_name:  rhel-edge-kvm
libvirt_image_dir: /var/lib/libvirt/images
libvirt_iso_dir:  /var/lib/libvirt/images
template_dir: "{{ iso_download_directory }}"
libvirt_defaults:
  edge_device:
    cpu: 2
    memory: 2097152 

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

**RHEL Username **
* Required: true  
* Question:`RH Username:` . 
* Answer variable name: `rh_authentication_basic_username` . 
![20221114204454](https://i.imgur.com/z0UsSCe.png)

**RHEL Password**
* Required: true   
* Question: `RH Password:` . 
* Answer variable name: `rh_authentication_basic_password` . 
![20221114204423](https://i.imgur.com/b9rxVMx.png)

**API Token:**
> [Red Hat API Tokens](https://access.redhat.com/management/api) . 
* Required: true  
* Question: `RH Password:` . 
* Answer variable name: `rh_offline_authentication_api_bearer_token` . 
![20221114204342](https://i.imgur.com/t6Eg7OJ.png)
![20221114204230](https://i.imgur.com/nxT5Fd7.png)

---

![20221114204258](https://i.imgur.com/X4wKMNY.png)
