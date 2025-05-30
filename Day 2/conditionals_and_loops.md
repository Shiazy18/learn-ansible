# Conditionals & Loops in Ansible

---

## Conditionals in Ansible

Conditionals let you control when a task should run. You use the `when` keyword to define conditions based on variables, facts, or results from other tasks.

### Basic `when` usage

```yaml
- name: Install Nginx on Ubuntu
  hosts: all
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
      when: ansible_facts['os_family'] == "Debian"
```

## Using registered variables in conditions

```yaml
- name: Check for file existence
  hosts: all
  tasks:
    - name: Stat the file
      stat:
        path: /tmp/myfile.txt
      register: file_status

    - name: Delete file if it exists
      file:
        path: /tmp/myfile.txt
        state: absent
      when: file_status.stat.exists
```

## Loops in Ansible

Loops are used to repeat a task with different items.

### Using Loops

```yaml
- name: Install multiple packages
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - git
    - curl
    - vim
```

### Loop with dictionaries or muliple loops

```yaml
- name: Create users with different shells
  user:
    name: "{{ item.name }}"
    shell: "{{ item.shell }}"
    state: present
  loop:
    - { name: 'alice', shell: '/bin/bash' }
    - { name: 'bob', shell: '/bin/zsh' }
```

### Loop with with_items (older syntax):

```yaml
- name: Add users
  user:
    name: "{{ item }}"
    state: present
  with_items:
    - devuser1
    - devuser2
```

## Combining when with loops

```yaml
- name: Install only selected packages
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - git
    - apache2
    - nginx
  when: item != "apache2"
```

## Summary

- Use when to apply logic and conditional execution of tasks.
- Use loop to repeat tasks for a list of values.
- Combine when and loop for more powerful automation.
- Prefer loop over older looping methods like with_items.