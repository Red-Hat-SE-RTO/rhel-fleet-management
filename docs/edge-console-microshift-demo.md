# MicroShift demo on the Edge Management console - WIP
> Contributions are welcome current work in progress
Deploy the MicroShift demo on the Edge Management console using Ansible Automation Platform. 

This demo will allow you to experience the integration between MicroShift and the RedHat hosted Edge fleet management. At the time of writing this demo, MicroShift is still in development, and it's impossible to bundle the MicroShift package into image builds yet. To make this possible, we use the public test build created by the MicroShift team for the KubeCon NA 2022 here in copr.

Link: https://github.com/redhat-et/microshift-demos/tree/main/demos/edge-console-demo

## Prerequisites
* Ansible Automation Platform 
* Build image job 
* Download ISO job 
* Deploy to KVM job
* [Create a custom repository](https://github.com/redhat-et/microshift-demos/tree/main/demos/edge-console-demo#create-a-custom-repository)


## Build Image Job Parameters
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
image_name: "mircoshift-11-15-2022-b1" # Example: "test-image-11-13-2022-b1"
username: "admin"
distribution: "rhel-86"
description: "sample description"
build_template: image-mircoshift-build # for standard deployments image-build
mircroshift_deployment: false
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
