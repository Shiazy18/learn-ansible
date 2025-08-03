# Facts and Register in Ansible

Ansible provides mechanisms to **gather system information** (facts) and **store task results** (register) for use in later tasks. These features allow playbooks to make dynamic decisions.

---

## What are Ansible Facts?

Facts are **system properties** collected from managed hosts (OS, IP, memory, etc.) using the `setup` module.

---

### View All Facts

```bash
ansible all -m setup
```

Or to filter specific facts:

```bash
ansible all -m setup -a 'filter=ansible_distribution*'
```

---

### Using Facts in Playbooks

```yaml
- name: Display OS info
  hosts: all
  tasks:
    - name: Show OS family
      debug:
        msg: "This system is based on {{ ansible_os_family }}"
```

Facts are available as variables with the `ansible_` prefix.

---

## Using `gather_facts`

By default, `gather_facts` is `true`. You can turn it off to speed up execution when facts aren’t needed.

```yaml
- hosts: all
  gather_facts: false
```

---

## Registering Task Results

The `register` keyword lets you **capture output** of a task into a variable.

---

### Basic Example

```yaml
- name: Register output
  hosts: localhost
  tasks:
    - name: Run a command
      command: "uname -r"
      register: kernel_result

    - name: Show result
      debug:
        var: kernel_result.stdout
```

---

### Structure of Registered Variable

The registered variable is a dictionary containing keys like:

- `stdout`, `stderr`
- `rc` (return code)
- `stdout_lines`, `stderr_lines`
- `changed`

You can access any of these for conditions or logic.

---

### Example: Conditional Task with Register

```yaml
- name: Conditional restart
  hosts: all
  tasks:
    - name: Check if service is active
      shell: systemctl is-active nginx
      register: nginx_status
      ignore_errors: true

    - name: Restart nginx if inactive
      service:
        name: nginx
        state: restarted
      when: nginx_status.stdout != "active"
```

---

## Tips

- Registered variables are local to the host they are run on.
- Use `debug` to inspect registered variables during development.
- You can chain with `with_items` or `loop` for multiple result handling.

---

## Summary

| Feature      | Purpose                             | Used For                        |
|--------------|-------------------------------------|---------------------------------|
| Facts        | Gather system info from hosts       | OS, IP, Memory, Disk, etc.      |
| Register     | Store task output for later use     | Logic, conditions, debugging    |

---

Mastering facts and register helps you make playbooks that are **context-aware** and **intelligent**, adapting to any environment!
