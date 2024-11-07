# Ansible Ubuntu server secure setup
[![ansible-lint](https://github.com/Avonae/ansible-playbooks/actions/workflows/ansible-lint.yml/badge.svg?branch=main)](https://github.com/Avonae/ansible-playbooks/actions/workflows/ansible-lint.yml)

This playbook allows you to configure Ubuntu quickly and securely. Assuming that [Ansible is already installed](https://docs.ansible.com/ansible/latest/installation_guide/) on your system.
The main actions performed by the playbook are:

- Changes the SSH port to a random one within the range 20000-30000
- Disables root authentication and password authentication
- Adds the server's IP, port, and username to ~/.ssh/config on the host machine
- Adds the SSH port to UFW and enables it
Additionally, you can also install updates. Once the setup is complete, you can log in using a simple command:

After installing you'll get a message with connection details:

![image](https://github.com/user-attachments/assets/17ab42bf-6fab-4f47-acd8-cd3fac92aa16)

```
ssh server_ip
```
And get connected via sudo user:

![image](https://github.com/user-attachments/assets/ada9fdca-c10c-4e49-b972-941dff3bf337)

The installation consist of 3 parts:

1. System configuration and Setup — tag `system_setup`
2. Secure SSH configuration — tag `ssh_setup`
3. User Profile Setup — tag `profile_update`

You can skip the `profile_update` and `ssh_setup` tags, but you can't skip `system_setup` because a user is created there which is used in the following roles.

```
ansible-playbook playbook.yml --tags "system_setup,ssh_setup"
```

# Usage
For default installation you should have a clean ubuntu server with `root` user available through SSH.

1. Download the repository:
```
git clone https://github.com/Avonae/ansible-playbooks.git
```
2. Change the directory:
```
cd ansible-playbooks
```
3. Change server IP address to yours in `inventory.ini` file
4. Change root password in `group_vars/all.yml` file
5. Start the installation 

# Default variables
The repository already have variables file. 



# System Configuration and Setup

This role configures core system settings such as hostname, timezone and logging.

1. Set Hostname
2. Set Timezone
3. Install Necessary Packages
4. Enable and Configure Logging
5. Disable Swap
6. User and SSH Port Management
7. Create Temporary Directories for the User
---
## Secure SSH Configuration

This role secures SSH access on the server by setting up RSA key-based authentication, and disabling root login and password-based authentication.

1. Ensure .ssh Directory
2. Generate SSH Key Pair
3. Add Public Key to Authorized Keys
4. Configure SSH Daemon for Security
5. Update UFW Rules
6. Configure Local SSH Client Settings
7. Manage SSH Service
8. Rollback on Failure

---

## User Profile Setup

This role installs Neovim, adds it to the user’s `PATH`, and customizes the user’s profile settings in `.bashrc` for enhanced productivity.

1. Download and Install Neovim
2. Configure `.bashrc` for User
3. Display Connection Information
4. Cleanup Temporary Password File

## Post tasks
Post tasks include 
1. Apt ugrade -y
2. Enabling UFW if you the the `ufw_enable` variable is set
