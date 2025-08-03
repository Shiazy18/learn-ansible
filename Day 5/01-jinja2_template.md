# Jinja2 Templating in Ansible

Jinja2 is a powerful templating engine used by Ansible to dynamically generate configuration files, scripts, and content. It allows you to use variables, control structures (like `if`, `for`), filters, and custom logic.

---

## Why Use Jinja2?

- Dynamically generate configuration files
- Avoid code repetition with loops
- Make templates reusable across environments
- Handle conditional logic in output files

---

## Basic Syntax

| Expression Type     | Example                              |
|---------------------|--------------------------------------|
| Variable            | `{{ variable_name }}`                |
| If Statement        | `{% if condition %} ... {% endif %}` |
| For Loop            | `{% for item in list %} ... {% endfor %}` |
| Filter              | `{{ variable | filter }}`            |

---

## Example: Nginx Configuration Template

**File: `nginx.conf.j2`**

```jinja2
server {
    listen 80;
    server_name {{ domain_name }};

    location / {
        proxy_pass http://{{ backend_host }}:{{ backend_port }};
    }

    {% if enable_logging %}
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
    {% endif %}
}
```

**Playbook Snippet:**

```yaml
- name: Template Nginx config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
```

**Variables Example:**

```yaml
domain_name: example.com
backend_host: app01
backend_port: 8080
enable_logging: true
```

---

## Loop Example

```jinja2
{% for user in users %}
- name: Create user {{ user }}
  user:
    name: "{{ user }}"
    state: present
{% endfor %}
```

Where `users` is a list:

```yaml
users:
  - alice
  - bob
  - charlie
```

---

## Filters Example

```jinja2
{{ 'hello world' | upper }}       # Output: HELLO WORLD
{{ mylist | join(', ') }}         # Output: item1, item2, item3
{{ some_number | int }}           # Converts string to integer
```

---

## Template Placement

Templates are usually stored in a `templates/` directory inside your Ansible role or playbook folder.

```
.
├── playbook.yml
├── templates/
│   └── nginx.conf.j2
```

---

## Best Practices

- Use descriptive variable names
- Use defaults in variables to avoid failures (`{{ var | default('value') }}`)
- Test templates with `ansible-playbook --check --diff`

---

## Bonus: Template with Register Variable

```yaml
- name: Generate config
  template:
    src: config.j2
    dest: /tmp/generated.conf
  register: config_result

- debug:
    var: config_result
```

---

> Templates + Jinja2 allow you to write less, reuse more, and scale better.
