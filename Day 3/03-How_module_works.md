# How Ansible Modules Work

Ansible modules are the building blocks of all Ansible tasks. They are small programs that perform specific actions like installing packages, copying files, managing users, or interacting with cloud platforms.

---

## What is an Ansible Module?

- A module is a standalone script written in Python (or other languages) that Ansible can execute on remote nodes.
- Ansible ships with **hundreds of modules** for system administration, cloud provisioning, networking, and more as discussed before.
- When a task is executed, Ansible runs the module on the target system via SSH or WinRM and collects the output.

---

## How Do Modules Work Internally?

1. **Playbook or Ad-hoc Task Triggers Module**
   - You define the module and its parameters in a playbook or ad-hoc command.
2. **Control Node Sends Module Code**
   - Ansible sends the module code + parameters to the managed node.
3. **Module Executes on Remote Machine**
   - It runs via SSH (Linux) or WinRM (Windows).
4. **Returns JSON Output**
   - The module exits with a JSON-formatted response.
   - Contains `changed`, `failed`, `msg`, and other fields.

---

## Example: `ping` Module Execution

```bash
ansible all -m ping
```

This sends the ping module to all hosts in the inventory.

Output:

```json
{
  "changed": false,
  "ping": "pong"
}
```

---

## Anatomy of a Module Call (Playbook Example)

```yaml
- name: Install nginx on Ubuntu
  hosts: webservers
  become: true
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

- `apt` is the module.
- `name` and `state` are its parameters.
- Ansible sends the required logic to the remote host and executes it.

---

## Idempotency in Modules

- Most Ansible modules are **idempotent**.
- Running the same task again doesn’t cause changes unless something actually changed.
- This ensures reliability and consistency.

---

## Writing Your Own Module (Simple Python Example)

```python
#!/usr/bin/python

from ansible.module_utils.basic import AnsibleModule

def main():
    module = AnsibleModule(argument_spec={})
    result = {"changed": False, "msg": "Hello from custom module!"}
    module.exit_json(**result)

if __name__ == '__main__':
    main()
```

Save this as a custom module and call it using the `script` or `command` module.

---

## Module Return Values

All modules return a dictionary in JSON with these keys:

- `changed`: Boolean indicating whether anything changed.
- `failed`: Boolean indicating failure.
- `msg`: Optional message.
- `rc`: Return code (for command modules).
- `stdout`, `stderr`: Output streams (for shell/command modules).

---

## Module Documentation

Ansible provides built-in documentation:

```bash
ansible-doc <module_name>
```

Example:

```bash
ansible-doc apt
```

---

## Summary

| Aspect            | Details                                                                 |
|-------------------|-------------------------------------------------------------------------|
| Language          | Mostly Python                                                           |
| Transport         | SSH (Linux/macOS), WinRM (Windows)                                      |
| Input             | Parameters via playbooks/ad-hoc                                         |
| Output            | JSON format                                                             |
| Benefits          | Reusable, idempotent, and consistent                                    |
| Examples          | `apt`, `yum`, `copy`, `user`, `service`, `command`, `shell`, `ec2`, etc. |

---
