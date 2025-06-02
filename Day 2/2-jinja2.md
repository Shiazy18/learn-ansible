# Templates using Jinja2 in Ansible

---

## What is a Template?

A **template** in Ansible is a text file with **dynamic content**, usually using the `.j2` extension (Jinja2 template). Templates allow you to insert variables and logic into files that will be rendered and deployed to target systems.

---

## Why use Templates?

- Create **dynamic config files** based on variables.
- Customize files for different environments or hosts.
- Make playbooks **reusable and flexible**.

---

## Jinja2 Syntax Overview

| Element         | Example                              |
|----------------|---------------------------------------|
| Variable        | `{{ var_name }}`                      |
| If condition    | `{% if condition %} ... {% endif %}` |
| Loop            | `{% for item in list %} ... {% endfor %}` |
| Comments        | `{# This is a comment #}`             |

---

## File Structure

├── templates
│ └── nginx.conf.j2
├── playbook.yml

---

## Template Example

### templates/nginx.conf.j2**

```jinja2
server {
    listen 80;
    server_name {{ server_name }};
    
    location / {
        proxy_pass http://{{ backend }};
    }
}
```

## Using Template in a Playbook

```yaml 
- name: Render NGINX config from template
  hosts: web
  vars:
    server_name: example.com
    backend: 127.0.0.1:5000
  tasks:
    - name: Generate nginx config
      template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/sites-available/default

```

## Templates with Loops and Conditionals

```jinja2
{% for user in users %}
user: {{ user.name }}
shell: {{ user.shell }}
{% if user.admin %}
role: admin
{% else %}
role: standard
{% endif %}

{% endfor %}
```

```vars
users:
  - name: alice
    shell: /bin/bash
    admin: true
  - name: bob
    shell: /bin/zsh
    admin: false

```

## Tips

- Use {{ }} for variables.
- Use {% %} for logic (loops, conditionals).
- Templates are best kept in the /templates folder.
- Always validate your output before applying it to production systems.

## Summary

- Templates make config files dynamic using Jinja2.
- Use the template module in playbooks to render .j2 files.
- Combine with variables, loops, and conditionals for flexibility.
- Great for rendering environment-specific files like NGINX, systemd, SSH config, etc.