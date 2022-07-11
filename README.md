# RHEL Fleet Manager
Use Ansible to manage RHEL instances using Fleet Manager or Image Builder. 


## Tasks:
* Hyper-V Role 
  * Load VM with iso and boot quarkuscofffeeshop 
* Build role for console.redhat.com
* perform updates of image from console.redhat.com
* Templatize the kickstart file for the different repos
* Create ansible configuration file for deployments.
* Show offline online Scenario
* pipe dream: fail back to cloud instance.  
* Tekton pipelines for build packs
* nice to have: tekton pipeline to trigger ansible job 
* Documentation 

## directory structure 
```
tree .         
.
├── README.md
├── inventories -> inventory files for one or more edge nodes
│   ├── edge1 -> this could point to one or more edge node based on the settings
│   │   ├── applications
│   │   │   └── quarkuscoffeeshop-majestic-monolith
│   │   │       ├── kickstart.ks
│   │   │       └── quarkuscoffeeshop-majestic-monolith.toml
│   │   ├── group_vars
│   │   ├── host_vars
│   │   └── hosts
│   ├── edge2
│   │   ├── applications
│   │   │   └── quarkuscoffeeshop-majestic-monolith
│   │   │       ├── kickstart.ks
│   │   │       └── quarkuscoffeeshop-majestic-monolith.toml
│   │   ├── group_vars
│   │   ├── host_vars
│   │   └── hosts
│   ├── edge3
│   │   ├── applications
│   │   │   └── quarkuscoffeeshop-majestic-monolith
│   │   │       ├── kickstart.ks
│   │   │       └── quarkuscoffeeshop-majestic-monolith.toml
│   │   ├── group_vars
│   │   ├── host_vars
│   │   └── hosts
│   └── lab
│       ├── applications
│       │   └── quarkuscoffeeshop-majestic-monolith 
│       │       ├── kickstart.ks
│       │       └── quarkuscoffeeshop-majestic-monolith.toml
│       ├── group_vars
│       ├── host_vars
│       └── hosts
├── roles -> add new roles here
│   ├── quarkuscoffeeshop-majestic-monolith-ansible
│   │   ├── README.md
│   │   ├── collections
│   │   │   └── requirements.yml
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── images
│   │   │   └── coffeeshop.png
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── tasks
│   │   │   ├── auto_update_image.yml
│   │   │   ├── aws_deployment.yaml
│   │   │   ├── azure_deployment.yaml
│   │   │   ├── configure-dev-enviornment.yml
│   │   │   ├── deploy_appication.yml
│   │   │   ├── deploy_appication_on_cloud.yml
│   │   │   ├── gcp_deployment.yaml
│   │   │   ├── main.yml
│   │   │   ├── openstack_deployment.yaml
│   │   │   ├── remove_application.yaml
│   │   │   ├── validate_azure_disk_size.yml
│   │   │   └── vmware_deployment.yaml
│   │   ├── templates
│   │   │   └── generate-systemd.sh.j2
│   │   ├── tests
│   │   │   ├── azure-deployment.yml
│   │   │   ├── cleanup-application.yml
│   │   │   ├── deploy-dev-enviornment-on-azure.yml
│   │   │   ├── deploy-dev-enviornment.yml
│   │   │   ├── inventory
│   │   │   ├── test.yml
│   │   │   └── update-quarkuscoffeeshop-image.yml
│   │   └── vars
│   │       └── main.yml
│   └── rhel-edge-mangement-role
│       ├── README.md
│       ├── collections
│       │   └── requirements.yml
│       ├── defaults
│       │   └── main.yml
│       ├── files
│       ├── handlers
│       │   └── main.yml
│       ├── meta
│       │   └── main.yml
│       ├── tasks
│       │   ├── ai-svc
│       │   │   └── setup_auth_headers.yaml
│       │   ├── build-image.yml
│       │   ├── main.yml
│       │   └── preflight
│       │       └── main.yaml
│       ├── templates
│       │   └── device-group.yaml.j2
│       ├── tests
│       │   ├── inventory
│       │   ├── test-offline-token.yml
│       │   └── test.yml
│       └── vars
│           └── main.yml
└── site.yml

44 directories, 55 files
```