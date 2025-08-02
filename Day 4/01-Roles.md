# Ansible Roles

## What are Roles?

Roles in Ansible help **organize playbooks** into reusable, modular components. They allow you to **structure your automation code** cleanly by separating variables, tasks, files, handlers, templates, and defaults.

A role is basically a **directory structure** with specific files in specific locations.

## Default Directory Structure

```bash
roles/
├── webserver/
│   ├── defaults/
│   │   └── main.yml
│   ├── files/
│   │   └── index.html
│   ├── handlers/
│   │   └── main.yml
│   ├── meta/
│   │   └── main.yml
│   ├── tasks/
│   │   └── main.yml
│   ├── templates/
│   │   └── nginx.conf.j2
│   └── vars/
│       └── main.yml
```

Each subdirectory has its own purpose:

| Directory     | Purpose |
|---------------|---------|
| `defaults/`   | Default variables (lowest precedence) |
| `vars/`       | Variables with higher precedence |
| `files/`      | Static files to be copied |
| `templates/`  | Jinja2 templates |
| `tasks/`      | List of tasks to execute |
| `handlers/`   | Notification handlers |
| `meta/`       | Role dependencies and metadata |

## 🛠 How to Use a Role in a Playbook

```yaml
- hosts: web
  roles:
    - webserver
```

This will automatically include everything defined in the `webserver` role (tasks, handlers, vars, etc.).

## Creating a Role with `ansible-galaxy`

You can scaffold a role using:

```bash
ansible-galaxy init <role-name>
```

Example:

```bash
ansible-galaxy init apache
```

This creates the full directory structure for your role.

## Ansible Galaxy

Ansible Galaxy is a **hub for finding and sharing roles**.

- Website: [https://galaxy.ansible.com](https://galaxy.ansible.com)
- Install roles directly:
  
```bash
ansible-galaxy install <namespace.role_name>
```

Example:

```bash
ansible-galaxy install geerlingguy.nginx
```

## Benefits of Roles

- Reusability
- Clean and scalable structure
- Easier collaboration
- Better separation of concerns

---

Roles are essential for writing scalable and maintainable Ansible code. As your projects grow, using roles becomes a best practice rather than a choice.
