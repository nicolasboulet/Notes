# Ansible cheatsheet

##### Table of Contents
[Install](#install)  
[Config](#config)  
[Command](#command)  
[Inventory](#inventory)  

<a name="install"/>

## Install  
```bash
sudo apt-get update
sudo apt-get install python-minimal virtualenv python-dev build-essential
```
### Vitualenv active and deactive, pip and ansible install

```bash
#create virtual environement active and desactive it
virtualenv venv27
source venv27/bin/activate
deactivate

#install desinstall ansible via pip
which pip
pip install ansible
ansible --version

pip uninstall ansible
ansible --version

#or install with git
sudo apt install git
pip install git+https://github.com/ansible/ansible

```

<a name="config"/>

## Config

### Config file precedence

1. ANSIBLE_CONFIG
2. ./ansible.cfg
3. ~/.ansible.cfg
4. /etc/ansible/ansible.cfg

```bash
touch /tmp/ANSIBLE_CONFIG.cfg
export ANSIBLE_CONFIG=/tmp/ANSIBLE_CONFIG.cfg

touch ./ansible.cfg

touch ~/.ansible.cfg

sudo mkdir /etc/ansible
sudo touch /etc/ansible/ansible.cfg
```

### Config ssh key => access to the hosts

```bash
#ssh-keygen -H -F centos1
#ssh-keygen -H -F 192.168.0.45

ssh-keygen #always answer with default options
ssh-copy-id centos1
```

### ansible.cfg

```bash
[defaults]
inventory = hosts.json #extension is important format (INI/JSON/YAML)
#store automaticaly ssh key
host_key_checking = False
```

<a name="command"/>

## Commande

### General 

```bash
## Documentation
ansible-doc debug

## Changing args
ansible all -m debug --args='msg="This is a custom debug message" verbosity=3'

### list hosts of group
ansible centos --list-hosts
```

### Ping
```bash
## Ping (all is host group)
ansible all -m ping

## Ping automaticaly store key for one time or see config ansible.cfg section for permanent settings
ANSIBLE_HOST_KEY_CHECKING=False ansible all -m ping

## Ping specifing on,e host of the group
ansible all -i centos1, -m ping

## Ping specifing host file
ansible all -i hosts.json -m ping

## Ping with result on only one line
ansible all -m ping -o
```

### Debug

```bash
ansible all -m debug
```

### You should known

```bash
ansible all -m ping
# Is equivalent to
ansible '*' -m ping
```

<a name="inventory"/>

## Inventory

### Select an user port for host

```bash
[control]
ubuntu-c ansible_connection=local  # local connection node-manager

[centos] # Group centos
centos1 ansible_user=root ansible_port=2222 # using the port 2222
centos2 ansible_user=root # host centos1 with user root
centos3:22 ansible_user=root # select the port 22 (for the example )

[ubuntu]
ubuntu1 ansible_become=true ansible_become_pass=password # log in regular user and ask to become sudo with specified password (ansible_become_password)
ubuntu2 ansible_become=true ansible_become_pass=password
ubuntu3 ansible_become=true ansible_become_pass=password
```

### use a range
 
```bash
[control]
ubuntu-c ansible_connection=local

[centos]
centos1 ansible_user=root ansible_port=2222
centos[2:3] ansible_user=root

[ubuntu]
ubuntu[1:3] ansible_become=true ansible_become_pass=password

```

### use a vars

```bash
[control]
ubuntu-c ansible_connection=local

[centos]
centos1 ansible_port=2222
centos[2:3]

[centos:vars]
ansible_user=root

[ubuntu]
ubuntu[1:3]

[ubuntu:vars]
ansible_become=true
ansible_become_pass=password
```

### use  children

```bash
[control]
ubuntu-c ansible_connection=local

[centos]
centos1 ansible_port=2222
centos[2:3]

[centos:vars]
ansible_user=root

[ubuntu]
ubuntu[1:3]

[ubuntu:vars]
ansible_become=true
ansible_become_pass=password

[linux:children]
centos
ubuntu
```
### YAML equivalent

```yaml
---
control:
  hosts:
    ubuntu-c:
      ansible_connection: local
centos:
  hosts:
    centos1:
      ansible_port: 2222
    centos2:
    centos3:
  vars:
    ansible_user: root
ubuntu:
  hosts:
    ubuntu1:
    ubuntu2:
    ubuntu3:
  vars:
    ansible_become: true
    ansible_become_pass: password
linux:
  children:
    centos:
    ubuntu:
...
```
### JSON equivalent

```json
{
    "control": {
        "hosts": {
            "ubuntu-c": {
                "ansible_connection": "local"
            }
        }
    },
    "ubuntu": {
        "hosts": {
            "ubuntu1": null,
            "ubuntu2": null,
            "ubuntu3": null
        },
        "vars": {
            "ansible_become": true,
            "ansible_become_pass": "password"
        }
    },
    "centos": {
        "hosts": {
            "centos3": null,
            "centos2": null,
            "centos1": {
                "ansible_port": 2222
            }
        },
        "vars": {
            "ansible_user": "root"
        }
    },
    "linux": {
        "children": {
            "centos": null,
            "ubuntu": null
        }
    }
}
```
