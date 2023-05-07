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
## Requirements setup ansible vault

### Create a vault password file
```
curl -OL https://gist.githubusercontent.com/tosin2013/022841d90216df8617244ab6d6aceaf8/raw/94bbcb5f08e4d1f8507cef935a8ba27c092bb85a/ansible_vault_setup.sh
chmod +x ansible_vault_setup.sh
./ansible_vault_setup.sh
```

### Install and run ansible safe
```
curl -OL https://github.com/tosin2013/ansiblesafe/releases/download/v0.0.6/ansiblesafe-v0.0.6-linux-amd64.tar.gz
tar -zxvf ansiblesafe-v0.0.6-linux-amd64.tar.gz
chmod +x ansiblesafe-linux-amd64 
sudo mv ansiblesafe-linux-amd64 /usr/local/bin/ansiblesafe
ansiblesafe -f 

```
# Tested on 
* Fedora 37

## Development Steps
```
git clone https://github.com/Red-Hat-SE-RTO/rhel-fleet-management.git
```


# Test inventory
```
ansible-navigator  inventory --list -m stdout --vault-password-file $HOME/.vault_password
```

## Deploy VM instances on KVM 
```
ansible-navigator run site.yml \
        --vault-password-file "$HOME"/.vault_password -m stdout  -t create_kvm_vm --skip-tags "create_device_group,build_image,get_build_status,download_latest_iso"
```

## Troubleshoting
```
"msg": "libvirtError: unsupported configuration: Emulator '/usr/libexec/qemu-kvm' does not support machine type 'pc-q35-rhel8.6.0'"

$ qemu-kvm -machine ?
```