# Ansible Roles for Ubuntu Server Setup and Configuration

This repository includes a series of Ansible roles designed to automate the setup and configuration of a server, with a focus on system settings, SSH configuration, and user environment customization. The roles are organized to be executed in the following order:

1. **System Configuration and Setup**
2. **Secure SSH Configuration**
3. **User Profile Setup**

## System Configuration and Setup

This role configures core system settings such as hostname, timezone and logging.

1. **Set Hostname**
2. **Set Timezone**
3. **Install Necessary Packages**
4. **Enable and Configure Logging**
5. **Disable Swap**
6. **User and SSH Port Management**
7. **Create Temporary Directories for the User**
---
## Secure SSH Configuration

This role secures SSH access on the server by setting up RSA key-based authentication, and disabling root login and password-based authentication.

1. **Ensure .ssh Directory**
2. **Generate SSH Key Pair**
3. **Add Public Key to Authorized Keys**
4. **Configure SSH Daemon for Security**
5. **Update UFW Rules**
6. **Configure Local SSH Client Settings**
7. **Manage SSH Service**
8. **Rollback on Failure**

---

## User Profile Setup

This role installs Neovim, adds it to the user’s `PATH`, and customizes the user’s profile settings in `.bashrc` for enhanced productivity.

1. **Download and Install Neovim**
2. **Configure `.bashrc` for User**
3. **Display Connection Information**
4. **Cleanup Temporary Password File**

## Post tasks
Post tasks include 
1. Apt ugrade -y
2. Enabling UFW if you the the `ufw_enable` variable is set

# Usage

