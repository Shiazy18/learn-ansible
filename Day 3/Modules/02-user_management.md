# User Management in Ansible

---

## Overview

Ansible makes it easy to **create**, **delete**, and **manage user accounts** across multiple systems.  
This is done using the **`user`** and **`authorized_key`** modules.

These modules are **idempotent**, meaning repeated runs won't create duplicate users or re-apply the same SSH key unnecessarily.

---

## Creating a User

```yaml
- name: Create a user named 'devops'
  ansible.builtin.user:
    name: devops
    state: present
    shell: /bin/bash
```

---

## Deleteing a User

```yaml
- name: Remove user 'devops'
  ansible.builtin.user:
    name: devops
    state: absent
    remove: yes   # This removes the home directory too

```

---

## Adding SSH Public Key

```yaml
- name: Add SSH key for 'devops'
  ansible.builtin.authorized_key:
    user: devops
    state: present
    key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
```

---

## Changing User Properties

```yaml
- name: Change shell and comment for user
  ansible.builtin.user:
    name: devops
    shell: /bin/zsh
    comment: "DevOps Engineer"
```

---

## Managing Home Directory

```yaml
- name: Create user with specific home directory
  ansible.builtin.user:
    name: devuser
    home: /data/devuser
    create_home: yes

```

---

## Managing Password

- Use mkpasswd --method=sha-512 or openssl passwd -6 to generate password hash.

```yaml
- name: Set user password (hashed)
  ansible.builtin.user:
    name: devuser
    password: "$6$rounds=5000$mysalt$g6Rgq...."
```

- Use mkpasswd --method=sha-512 or openssl passwd -6 to generate password hash.

---

## Best Practice 

- Avoid using plaintext passwords in playbooks.
- Use variables and vault to store secrets.
- Prefer SSH key authentication over password login.
- Always test user creation on a non-production host first.

---

To find list of all ansible modules, refer to Ansible documentation: https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html