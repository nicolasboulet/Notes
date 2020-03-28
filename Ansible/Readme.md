# Ansible cheatsheet

##### Table of Contents
[Install](#install)  
[Config](#config)

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

<a name="install"/>

##Config

###Config file precedence

1. ANSIBLE_CONFIG
2. ./ansible.cfg
3. ~/.ansible.cfg
4. /etc/ansible/ansible.cfg

