# 🗂️ Ansible Inventory Files

Ansible uses **inventory files** to define the hosts (servers or devices) that automation tasks should run against. You can group hosts, assign variables, and use static or dynamic methods to manage inventory.

---

## 🔸 Types of Inventory Files

### 1. **Static Inventory**
- Manually defined list of IPs or hostnames
- Written in **INI** or **YAML** format
- Best for small-scale or testing environments

### 2. **Dynamic Inventory**
- Generated from cloud providers (like Azure, AWS, GCP)
- Ideal for **cloud-based**, **dynamic** infrastructures
- Written using inventory **scripts** or **plugins**

---

## 📄 Static Inventory (INI Format)

### 🧪 Basic Example

```ini
[web]
web1 ansible_host=192.168.1.10 ansible_user=ubuntu
web2 ansible_host=192.168.1.11 ansible_user=ubuntu

[db]
db1 ansible_host=192.168.1.12 ansible_user=root
```

### Group varibales

```ini
[web:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### Nested Group 

```ini
[production:children]
web
db
```

### Static Inventory (YAML Formal)

```
all:
  children:
    web:
      hosts:
        web1:
          ansible_host: 192.168.1.10
          ansible_user: ubuntu
        web2:
          ansible_host: 192.168.1.11
          ansible_user: ubuntu
    db:
      hosts:
        db1:
          ansible_host: 192.168.1.12
          ansible_user: root
```
---

### Dynamic Inventory 

**Dynamic inventory** is generated at runtime using scripts or plugins that fetch host info from external systems like:
- AWS EC2
- Azure Resource Manager
- GCP
- VMware, OpenStack, etc.

### 🔹 Example: Azure Dynamic Inventory Plugin

### yaml

```
plugin: azure_rm
include_vm_resource_groups:
  - myResourceGroup
auth_source: auto
```


