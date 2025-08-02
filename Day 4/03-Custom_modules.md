# Custom Ansible Modules

While Ansible provides hundreds of built-in modules, sometimes you need to write your own to meet specific requirements. Custom modules allow you to extend Ansible's functionality using any language, typically Python.

---

## Why Create a Custom Module?

- No built-in module for your use case.
- You want to interact with a custom API or service.
- You want reusable, parameterized logic in your playbooks.

---

## Directory Structure

Custom modules can be stored in a `library/` directory at the root of your project:

``` file
project/
├── playbook.yml
└── library/
    └── my_custom_module.py
```

Ansible automatically loads modules from the `library/` folder.

---

## Basic Python Custom Module Example

### `my_custom_module.py`

```python
#!/usr/bin/python

from ansible.module_utils.basic import AnsibleModule

def run_module():
    module_args = dict(
        name=dict(type='str', required=True)
    )

    result = dict(
        changed=False,
        message=''
    )

    module = AnsibleModule(
        argument_spec=module_args,
        supports_check_mode=True
    )

    name = module.params['name']
    result['message'] = f"Hello, {name}!"

    module.exit_json(**result)

def main():
    run_module()

if __name__ == '__main__':
    main()
```

Make sure the file is executable:

```bash
chmod +x library/my_custom_module.py
```

---

## Playbook to Use Custom Module

```yaml
---
- name: Test custom module
  hosts: localhost
  tasks:
    - name: Say hello using custom module
      my_custom_module:
        name: Shivam
```

---

## Testing a Module Without a Playbook

```bash
ansible localhost -m my_custom_module -a "name=Shivam" -i localhost,
```

---

## Tips for Writing Modules

- Always use `AnsibleModule` from `ansible.module_utils.basic`.
- Support `check_mode` if possible.
- Use `exit_json()` to return results.
- Use `fail_json()` for error handling.
- Return structured output (dictionaries).

---

## Advanced Ideas

- Use external Python packages via `requirements.txt`.
- Interact with cloud APIs, databases, file systems.
- Raise meaningful errors using `fail_json(msg="Error message")`.

---

## Summary

| Component           | Description                                |
|---------------------|--------------------------------------------|
| `library/` folder   | Store custom module files                  |
| `AnsibleModule`     | Handles input, validation, and output      |
| `exit_json()`       | Successful return                          |
| `fail_json()`       | Return on failure                          |
| `--module-path`     | Run module from custom location            |

---

Custom modules give you the power to adapt Ansible to any environment. Start with simple examples, build reusable modules, and contribute back to the community when possible!
