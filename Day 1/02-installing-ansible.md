# Installing Ansible

<https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html>

## On Ubuntu/Debian

```bash
sudo apt update
sudo apt install ansible -y

#### On RHEL/CentOS:
```bash
sudo yum install epel-release -y
sudo yum install ansible -y

#### On MacOS:
```bash
brew install ansible

#### Verify:
```bash
ansible --version
