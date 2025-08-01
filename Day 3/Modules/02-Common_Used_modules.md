# Commonly Used Modules

This document provides a deep dive into the most commonly used Ansible modules, with basic syntax, usage examples, and tips.

## ping 

- Use: To test the connection with managed nodes.

```yml
- name: Test connectivity
  ansible.builtin.ping:
```
---

## command

- Use: Executes a command on the remote host.

```yaml
- name: Run a command
  ansible.builtin.command: ls -l /tmp
```

- Doesn’t support shell features like pipes, redirection

---

## shell

- Use: Runs shell commands with full shell features.
  
```yaml
- name: Run a shell script
  ansible.builtin.shell: "echo hello | tee /tmp/hello.txt"
```

---

## yum / apt

- Use: Installs/removes packages on RHEL/Debian systems.

```yaml
# For CentOS/RHEL
- name: Install nginx
  ansible.builtin.yum:
    name: nginx
    state: present

# For Ubuntu/Debian
- name: Install nginx
  ansible.builtin.apt:
    name: nginx
    state: present
    update_cache: yes
```

---

## stat

- Use: Checks file or directory status.

```yaml

- name: Check if a file exists
  ansible.builtin.stat:
    path: /tmp/hello.txt
  register: file_stat

- name: Display file existence
  ansible.builtin.debug:
    msg: "File exists"
  when: file_stat.stat.exists
```

---

## set_fact

- Use: Dynamically sets variables during playbook execution.

```yaml
- name: Set a dynamic variable
  ansible.builtin.set_fact:
    dynamic_var: "value"
```

---

## include_tasks / import_tasks

- Use: Reuse task files in playbooks.

```yaml
- name: Include task
  ansible.builtin.include_tasks: tasks/common.yml
```

---

## lineinfile

- Use: Ensures a line is present in a file.

```yaml
- name: Add config to file
  ansible.builtin.lineinfile:
    path: /etc/myapp.conf
    line: 'max_connections=100'
```

---

##  template

- Use: Renders a Jinja2 template on the remote host.

```yaml
- name: Deploy config from template
  ansible.builtin.template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
```
