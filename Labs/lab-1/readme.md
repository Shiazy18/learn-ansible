# Lab 1

## What's Covered

- Installing Ansible
- Create an inventory file
- Run a basic Ansible command

## Installing Ansible

### In Mac

```bash
# Install pip if not installed
sudo apt install python3-pip -y   # Ubuntu/Debian
# OR
brew install python               # macOS

# Install Ansible
pip3 install ansible --user

# Verify installation
ansible --version
```

### on Windows

Recommended: Use Windows Subsystem for Linux (WSL) so Ansible works like Linux.

```pwsh
# Install WSL (only if not installed)
wsl --install

# Inside WSL Ubuntu terminal
sudo apt update && sudo apt upgrade -y
sudo apt install python3-pip -y
pip3 install ansible --user

# Verify
ansible --version
```

