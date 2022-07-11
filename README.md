# RHEL Fleet Manager
Use Ansible to manage RHEL instances using Fleet Manager or Image Builder. 


## Tasks:
* Hyper-V Role 
  * Load VM with iso and boot quarkuscofffeeshop 
* Build role for console.redhat.com
* perform updates of image from console.redhat.com
* Templatize the kickstart file for the different repos
* Create ansible configuration for tower deployments.
* Show offline online Scenario
* pipe dream: fail back to cloud instance.  
* Tekton pipelines for build packs
* nice to have: tekton pipeline to trigger ansible job 
* Documentation 

## directory structure 
```
$ tree .
.
├── README.md
├── inventories  -> inventory files for one or more edge nodes
│   ├── edge1 -> this could point to one or more edge node based on the settings
│   │   ├── applications
│   │   │   └── quarkuscoffeeshop-majestic-monolith
│   │   │       ├── kickstart.ks
│   │   │       └── quarkuscoffeeshop-majestic-monolith.toml
│   │   └── hosts
│   ├── edge2
│   │   ├── applications
│   │   │   └── quarkuscoffeeshop-majestic-monolith
│   │   │       ├── kickstart.ks
│   │   │       └── quarkuscoffeeshop-majestic-monolith.toml
│   │   └── hosts
│   ├── edge3
│   │   ├── applications
│   │   │   └── quarkuscoffeeshop-majestic-monolith
│   │   │       ├── kickstart.ks
│   │   │       └── quarkuscoffeeshop-majestic-monolith.toml
│   │   └── hosts
│   └── lab
│       ├── applications
│       │   └── quarkuscoffeeshop-majestic-monolith
│       │       ├── kickstart.ks
│       │       └── quarkuscoffeeshop-majestic-monolith.toml
│       └── hosts
├── roles
│   └── requirements.yml -> add any required ansible roles 
└── site.yml

14 directories, 15 files
```