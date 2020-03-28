# Ansible cheatsheet

##### Table of Contents
[Install](#install)  

<a name="install"/>

## Install  
```bash
sudo apt-get update
sudo apt-get install python-minimal virtualenv python-dev build-essential
```
### Vitual env, pip, how select ansible version active an deactive

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
