# 📘 Day 3: Ansible Modules

---

## What Are Ansible Modules?

Ansible **modules** are the building blocks of Ansible.  
They are **small programs** (usually Python scripts) that run on the **target machines** (managed nodes) to perform specific tasks like installing packages, managing files, users, services, etc.

When you write a task in a playbook, you're essentially calling a module with specific arguments.

---

## Types of Modules

- **Core Modules** – Officially supported by Ansible and included by default.
- **Extras Modules** – Community-maintained modules.
- **Custom Modules** – You can create your own in Python or other languages.
- **Cloud Modules** – Specialized modules to manage cloud resources (e.g., Azure, AWS).

---

## How Modules Work

- Playbooks contain **tasks** that invoke **modules**.
- When you run a playbook:
  - Ansible copies the module code to the remote node.
  - Executes the module via **SSH** (or WinRM for Windows).
  - Removes the module after execution.
- Ansible is **agentless**—no software needs to be installed on the target host.

---

## Commonly Used Modules

| Module         | Description                                 |
|----------------|---------------------------------------------|
| `file`         | Create/delete files, set permissions        |
| `copy`         | Copy files from control to managed nodes    |
| `template`     | Deploy Jinja2 templates                     |
| `command`      | Run commands on remote hosts (no shell)     |
| `shell`        | Run shell commands (use with caution)       |
| `debug`        | Print variables/messages for debugging      |
| `lineinfile`   | Manage lines in text files                  |
| `stat`         | Get file or path information                |

---

## User Management

```yaml
- name: Add user
  ansible.builtin.user:
    name: devops
    shell: /bin/bash

- name: Add SSH key for devops
  ansible.builtin.authorized_key:
    user: devops
    key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
```

## Package Management

- Use apt for Debian/Ubuntu
- Use yum or dnf for Red Hat/CentOS

```yaml
- name: Install nginx using apt
  ansible.builtin.apt:
    name: nginx
    state: present
    update_cache: yes
```

## Service Management

```yaml
- name: Start nginx service
  ansible.builtin.service:
    name: nginx
    state: started
    enabled: yes
```

## Tips

- Always use modules instead of shell/command when available.
- Modules are idempotent, you can run them multiple times safely.
- Check module docs with:

```php
ansible-doc <module_name>
```
