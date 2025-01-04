# Ansible Home

This is my new Ansible home environment based on a Proxmox node, and provisioned using the ansible-proxmox repository.

Within the ansible-proxmox repo, the physical hosts are provisioned, and the VMs created
and this repo here, provisions the VMs after the initial setup is done using cloud-init.

The goal is to have a reproducible environment, that is easy to extend.

## Inventory
The inventory is based on a dynamic Proxmox inventory, using tags as groups. This way adding new hosts to Ansible is done automatically, and no further steps are necessary.
For hosts not provisioned by proxmox, they need to be added to `inventory/hosts`.

## Passwords
For now all passwords/credentials are stored in Ansible vaults, this includes the Proxmox credentials used for the dynamic inventory.

## Templating:
User https://j2live.ttl255.com/ to validate your templates

## Getting started

```
# create a venv
python3 -m venv ./venv

source ./venv/bin/activate

# install python requirements
pip install -r requirements.txt

# deactivate source and re-spurce it since sommetimes it has troubles
deactivate
source ./venv/bin/activate

# check if ansible is correctly loadet
ansible --version

# install neccesary roles and collections
ansible-galaxy install -r requirements.yml
```

This repo uses the site.yml as entrypoint for the playbooks:

```
ansible-playbook site.yml

# use --diff to see the changes
# use --check to make a dry runn
ansible-playbook site.yml --check --diff
```

To get the dynamically created inventory, run:
```
ansible-inventory --list
```
