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

### Select an user for host

```yaml
[centos] # Group centos
centos1 ansible_user=root # host centos1 with user root
centos2 ansible_user=root
centos3 ansible_user=root

[ubuntu]
ubuntu1 ansible_become=true ansible_become_pass=password # log in regular user and ask to become root with password password
ubuntu2 ansible_become=true ansible_become_pass=password
ubuntu3 ansible_become=true ansible_become_pass=password
```
