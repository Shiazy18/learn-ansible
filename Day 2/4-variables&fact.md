# Variables & Facts in Ansible

---

## Variables

Variables allow you to make your playbooks dynamic and reusable. You can define variables in multiple places such as:

- Inside the playbook (`vars` block)
- In inventory files
- As command-line arguments
- In separate variable files

### Defining variables in a playbook

```yaml
- name: User creation example
  hosts: all
  vars:
    username: devuser
    home_dir: "/home/devuser"
  tasks:
    - name: Create a user
      user:
        name: "{{ username }}"
        home: "{{ home_dir }}"
        state: present
```

### Defining variables in a separate file

```yaml
username: devuser
home_dir: /home/devuser
```

Then use it in your playbook like

```yaml
vars_files:
  - vars/users.yml
```

## Facts

Ansible automatically gathers system information (called facts) when a playbook runs. These facts can be used in conditions, templates, or logic.

### Example Usage  

```yaml
- name: Print OS Distribution
  hosts: all
  tasks:
    - name: Show distribution
      debug:
        var: ansible_facts['distribution']
```

### Disabling fact gathering (for faster playbook runs)

```yaml
- name: Playbook without facts
  hosts: all
  gather_facts: no
  tasks:
    - name: Dummy task
      debug:
        msg: "Facts gathering disabled"
```

## Accessing common facts

```yaml
ansible_facts['hostname']
ansible_facts['os_family']
ansible_facts['default_ipv4']['address']
```

To list all available facts:

```yaml
ansible all -m setup
```

## Summary

- Use variables for flexibility and reusability
- Use facts to write intelligent logic based on host details
- Facts are auto-collected but can be disabled
- Always use Jinja2 syntax ({{ }}) to reference variables and facts
