# Tags in Ansible Playbooks

---

## What are Tags?

Tags allow you to **selectively run** specific parts of your playbook without executing the entire playbook.

They are useful when you want to:

- Run only certain tasks for testing.
- Skip heavy or destructive operations.
- Execute fast iterative changes.

---

## Where Can You Use Tags?

You can apply tags to:

- Tasks
- Roles
- Blocks
- Handlers

---

## Adding Tags to Tasks

```yaml
- name: Install Nginx
  apt:
    name: nginx
    state: present
  tags: install

- name: Copy config file
  copy:
    src: nginx.conf
    dest: /etc/nginx/nginx.conf
  tags:
    - config
    - reload
```

## Running Tagged Tasks Only

Use --tags to run only tasks with specific tags:

```bash
ansible-playbook site.yml --tags install
```

## Skipping Tags

Use --skip-tags to run all tasks except those with the given tags:

```bash 
ansible-playbook site.yml --skip-tags reload
```

## Tagging Entire Plays

```yaml
- name: Install and configure web server
  hosts: web
  tags: webserver
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
```

## Tags with Blocks

```yaml
tasks:
  - block:
      - name: Create app user
        user:
          name: appuser
          state: present
      - name: Setup SSH key
        authorized_key:
          user: appuser
          key: "{{ lookup('file', 'id_rsa.pub') }}"
    tags: user_setup
```

## Best Practices

Use meaningful, consistent tag names.
Avoid over-tagging every single task unless necessary.
Use tags for:

- install, config, restart, backup, cleanup, test, etc.
Combine tags with handlers, templates, etc. for powerful workflows.

## Summary

- Tags give you granular control over playbook execution.
- Run or skip specific tasks using --tags or --skip-tags.
- Boosts efficiency during testing and debugging.
- Works on tasks, roles, blocks, and handlers.
