# Lookups and Filters in Ansible

Ansible provides **lookups** and **filters** to fetch external data and transform variables, making playbooks dynamic and powerful.

---

## Lookups

Lookups **pull in data from outside Ansible**, such as files, environment variables, or secrets.

### Syntax

```yaml
{{ lookup('plugin_name', 'term') }}
```

---

### Common Lookup Plugins

| Plugin         | Description                                 | Example                                      |
|----------------|---------------------------------------------|----------------------------------------------|
| `file`         | Read content from a local file              | `{{ lookup('file', 'secret.txt') }}`         |
| `env`          | Get environment variable                    | `{{ lookup('env', 'HOME') }}`                |
| `password`     | Generate or retrieve a password             | `{{ lookup('password', '/tmp/pwdfile') }}`   |
| `pipe`         | Run a shell command                         | `{{ lookup('pipe', 'date') }}`               |
| `csvfile`      | Lookup values from a CSV file               | `{{ lookup('csvfile', 'key file=map.csv') }}`|

---

### Lookup Example in Playbook

```yaml
- name: Using lookups
  hosts: localhost
  vars:
    secret_value: "{{ lookup('file', 'secret.txt') }}"
  tasks:
    - debug:
        msg: "The secret is: {{ secret_value }}"
```

---

## Filters

Filters are used to **modify or transform** variable values. They are based on Jinja2 filters and can be chained.

### 🛠️ Syntax

```yaml
{{ variable | filter_name }}
{{ variable | filter1 | filter2 }}
```

---

### Common Filters

| Filter        | Description                           | Example                                     |
|---------------|---------------------------------------|---------------------------------------------|
| `default`     | Set default if variable is undefined  | `{{ myvar | default('default_value') }}`    |
| `upper`       | Convert to uppercase                  | `{{ 'hello' | upper }}`                     |
| `lower`       | Convert to lowercase                  | `{{ 'HELLO' | lower }}`                     |
| `replace`     | Replace string patterns               | `{{ 'abc' | replace('a','z') }}`            |
| `join`        | Join list into string                 | `{{ ['a', 'b'] | join(',') }}`              |
| `unique`      | Remove duplicates from list           | `{{ [1,2,2,3] | unique }}`                  |
| `length`      | Get length of list/string             | `{{ mylist | length }}`                     |
| `dict2items`  | Convert dict to list of items         | `{{ mydict | dict2items }}`                 |

---

### Filter Example in Playbook

```yaml
- name: Using filters
  hosts: localhost
  vars:
    name: "shivam"
  tasks:
    - debug:
        msg: "Uppercase name: {{ name | upper }}"
```

---

## Combining Lookups and Filters

```yaml
- name: Lookup + filter
  hosts: localhost
  vars:
    file_contents: "{{ lookup('file', 'sample.txt') | upper }}"
  tasks:
    - debug:
        msg: "Contents: {{ file_contents }}"
```

---

## Tips

- Use `default` filter to avoid undefined variable errors.
- You can chain filters to transform data step by step.
- Lookup plugins are **only executed on the control node**.

---

## Summary

| Concept | Purpose                          | Executed On     |
|--------|----------------------------------|-----------------|
| Lookup | Fetch external/local data        | Control Node    |
| Filter | Transform variable values        | Managed Node    |

---

Mastering lookups and filters helps you write **cleaner, more dynamic** playbooks that adapt to real-world use cases.
