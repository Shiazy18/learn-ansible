# 📒 Playbook Basics and YAML Syntax

Ansible Playbooks are the core of automation — they define tasks to run on target hosts.

## 🧾 Basic YAML Syntax

- Uses `.yml` or `.yaml` extension
- Indentation matters (use spaces, not tabs)
- Key-value pairs and lists

## ▶️ Sample Playbook

```yaml
---
- name: Install Nginx on web servers
  hosts: web
  become: yes

  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

- hosts: Target group or hosts

- become: Run tasks with sudo/root

- tasks: A list of operations

- name: Description of the task