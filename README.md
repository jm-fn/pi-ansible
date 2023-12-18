# Raspberry Pi Ansible Configuration

This repository contains playbook for configuration of fresh install of Raspberry Pi OS, that was installed by [rpi-imager](https://github.com/raspberrypi/rpi-imager). The playbook makes changes to the configuration of Raspberry Pi OS that should harden the system and set up the system for use.

We assume that the image was created with a new user and with a public ssh key authentication.

# Setting up the repository
To set up this repo create a virtual environment, activate it and install ansible:
```
python3 -m venv .venv
.venv/bin/activate
pip3 install ansible
```

# Creating inventory
Following the template in `inventory/template.yml` create an inventory file. Encrypt the `ansible_become_password` with:
```
ansible-vault encrypt_string --vault-id ${my-vault-name}@prompt '<user_password_here>' --name 'ansible_become_password' 
```
Where `my-vault-name` is arbitrary name given to the vault (eq. `first_pi`).

# Running the playbooks
To run the playbooks use:
```
ansible -i inventory/<your_inventory_file>.yml --vault-id ${my-pi-name}@prompt pi-config.yml 
```
Where `my-vault-name` is the same as in the preceding paragraph.
