# Ubuntu server Ansible secure setup
[![ansible-lint](https://github.com/Avonae/ansible-playbooks/actions/workflows/ansible-lint.yml/badge.svg?branch=main)](https://github.com/Avonae/ansible-playbooks/actions/workflows/ansible-lint.yml)

This playbook allows you to configure Ubuntu quickly and securely. Assuming that [Ansible has been already installed](https://docs.ansible.com/ansible/latest/installation_guide/) on your system.
The main actions performed by the playbook are:

- Changes the SSH port to a random one within the range 20000-30000
- Disables root authentication and password authentication
- Adds the server's IP, port, and username to ~/.ssh/config on the host machine
- Adds the SSH port to UFW and enables it
Additionally, you can also install updates. 

The installation consist of 3 parts:

1. System configuration and Setup — tag `system_setup`
2. Secure SSH configuration — tag `ssh_setup`
3. User Profile Setup — tag `profile_update`

You can skip the `profile_update` and `ssh_setup` tags, but you can't skip `system_setup` because a user is created there which is used in the following roles.

```shell
ansible-playbook playbook.yml --tags "system_setup,ssh_setup"
```

# Usage
For default installation you should have a clean ubuntu server with `root` user available through SSH.

1. Download the repository:
```shell
git clone https://github.com/Avonae/ansible-playbooks.git
```
2. Change the directory:
```shell
cd ansible-playbooks
```
3. Change server IP address to yours in `inventory.ini` file
4. Change root password in `group_vars/all.yml` file
5. Start the installation 
```shell
ansible-playbook playbook.yml
```
After installing you'll get a message with connection details:

![image](https://github.com/user-attachments/assets/17ab42bf-6fab-4f47-acd8-cd3fac92aa16)

```shell
ssh server_ip
```
And get connected via sudo user:

![image](https://github.com/user-attachments/assets/ada9fdca-c10c-4e49-b972-941dff3bf337)

That's it.
If you want detailed output, uncomment this line in `ansible.cfg`:
```yaml
verbosity = 2 #uncomment this if you want to show detailed information
```

# Default variables
The repository already have variables file in `group_vars/all.yml` like:
```yaml
# domain_name:
super_user: "root"
server_user: "user" # Put name of your sudo user here
ssh_old_port: 22
time_zone: "Asia/Tbilisi" # Put your timezone here. This is Linux timezone format 
enable_ufw: true
update_install: false # Enable this if you want apt update && apt upgrade will will be executed. Please note that this may take a long time.
necessary_packages:
  - htop # and other packages
```
Change them for your needs.

# What exactly does the playbook do?
Detailed list of actions below.

## System Configuration and Setup

This role configures core system settings such as hostname, timezone and logging.

1. Set Hostname
2. Set Timezone
3. Install Necessary Packages an enable rsyslog
4. Disable Swap
5. Create user and adding it to `sudo` group

---
## Secure SSH Configuration

This role secures SSH access on the server by setting up RSA key-based authentication, and disabling root login and password-based authentication.

1. Generate SSH Key Pair
3. Add Public Key to Authorized Keys
4. Disable SSH socket daemon and enable SSH old-fashioned service
5. Adding new generated SSH port to UFW
6. Adding user, port, IP-address and private kay to ~/.ssh/config file on host machine
7. Restarting SSH Service

---

## User Profile Setup

This role installs Neovim, adds it to the user’s `PATH`, and customizes the user’s profile settings in `.bashrc` for enhanced productivity.

1. Neovim installation
2. Activating `.bashrc` aliases and make alias for vim=nvim

## Post tasks
Post tasks include 
1. Apt ugrade -y
2. Enabling UFW if you the the `ufw_enable` variable is set
