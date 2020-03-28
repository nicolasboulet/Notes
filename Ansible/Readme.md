# Ansible cheatsheet

##### Table of Contents
[Install](#install)  
[Config](#config)
[Command](#command)

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
```

### Ping
```bash
## Ping (all is host group)
ansible all -m ping

## Ping automaticaly store key for one time or see config ansible.cfg section for permanent settings
ANSIBLE_HOST_KEY_CHECKING=False ansible all -m ping

## Ping whitout use hosts inventory file but spoecifing it in the command
ansible all -i centos1, -m ping

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
