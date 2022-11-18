# AAP Install for development

Instructions for installing AAP for development purposes. Please see offical documentation for production installs.

https://access.redhat.com/management/api

### Deploy Jumpbox
> Red Hat Enterprise Linux 9.0 Update KVM Guest Image
```
sudo ssh-keygen

sudo kcli create vm -p rhel9_ansible ansible-aap --wait
```

### Crete Ansible AAP VM
```
sudo kcli ssh ansible-aap
```

### Configure RHEL 9 system
```        
curl -OL https://gist.githubusercontent.com/tosin2013/695835751174d725ac196582f3822137/raw/8bc48c73781fc744fbb1999ae7aeac7df3441c43/configure-rhel9.x.sh
chmod +x configure-rhel9.x.sh
./configure-rhel9.x.sh

```

### Clone AgnosticD repo
```                     
git clone https://github.com/redhat-cop/agnosticd.git
cd $HOME/agnosticd/ansible
git checkout development
```

### Create hosts file for inventory
```
cat >hosts<<EOF
localhost   ansible_connection=local
EOF
```

### create playbook to download the AAP tar file
```
cat >run_me.yaml<<EOF
- name: Install Ansible automation controller
  hosts: localhost
  gather_facts: false
  become: true

  tasks:
    - name: Install Ansible automation controller
      include_role:
        name: aap_download                     
EOF
```                    
                      
### create vars file for ansible playbook 
* Get offline token
> [Red Hat API Tokens](https://access.redhat.com/management/api)
* Update provided_sha_value if needed
* [Download Red Hat Ansible Automation Platform](https://access.redhat.com/downloads/content/480/ver=2.2/rhel---9/2.2/x86_64/product-software)
![](https://i.imgur.com/E8RQ2E3.png)

```
$ vi $HOME/offline_token
offline_token=$(cat $HOME/offline_token)
cat >dev.yml<<EOF
---
offline_token: '$(cat $HOME/offline_token)'
provided_sha_value: 9a90a8db350b2852471aa987f8487ace7bba85d64219221b5a613647a202e6c1
EOF

```

### Run Ansible Playbook to download AAP
```
ansible-playbook -i hosts run_me.yaml --extra-vars @dev.yml
```
### Extract aap file
```
tar -zxvf aap.tar.gz 
cd ansible-automation-platform-setup-bundle-2.2.1-1.1/
```
### Deploy Single Instance of AAP
```
$ export REGISTRY_USERNAME=""
$ export REGISTRY_PASSWORD=""
$ VM_IP_ADDRESS=$(hostname -I | awk '{print $1}')
$ cat >inventory<<EOF
[automationcontroller]
${VM_IP_ADDRESS} ansible_connection=local

[database]

[all:vars]
admin_password='$(openssl rand -base64 12)'

pg_host=''
pg_port=''

pg_database='awx'
pg_username='awx'
pg_password='$(openssl rand -base64 12)'

registry_url='registry.redhat.io'
registry_username='${REGISTRY_USERNAME}'
registry_password='${REGISTRY_PASSWORD}'
EOF
$ sudo ./setup.sh
```

### Get login information 
WEBPAGE: https://youripaddress
USERNAME: `admin`
```
 cat inventory  | grep admin_password
```

### You should see the Virtual Machine in Cockpit Dashboard
![](https://i.imgur.com/zR7pAed.png)
