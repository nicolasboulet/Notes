# Ansible cheatsheet

##### Table of Contents
[Install](#install)  

<a name="install"/>

## Install  
```bash
sudo apt-get update
sudo apt-get install python-minimal virtualenv python-dev build-essential
```
### Vitual env, pip, how select ansible version

```bash
virtualenv myenv27
source venv27/bin/activate
which pip
pip install ansible
ansible --version
pip uninstall ansible
ansible --version
sudo apt install git
pip install git+https://github.com/ansible/ansible

```
