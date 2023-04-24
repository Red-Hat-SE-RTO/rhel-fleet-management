# RHEL Fleet Manager
Use Ansible to manage RHEL instances using Fleet Manager or Image Builder. 

## Documentation
[Fleet Manager with AAP Documentation](docs/README.md)

[![ansible-lint](https://github.com/Red-Hat-SE-RTO/rhel-fleet-management/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/Red-Hat-SE-RTO/rhel-fleet-management/actions/workflows/ansible-lint.yml)

## Directory Structure 
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
