# Handlers in Ansible

---

## What are Handlers?

Handlers are special tasks that **run only when notified** by another task. They are typically used to perform actions that should occur only if a change is made — for example, restarting a service only if a configuration file changes.

Think of them as “delayed reactions” triggered when needed.

---

## Why use Handlers?

- Prevent unnecessary restarts or reloads.
- Ensure services are only impacted when changes are actually made.
- Improve performance and idempotency.

---

## Basic Handler Example

```yaml
- name: Install and configure Apache
  hosts: all
  become: yes
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present

    - name: Update config file
      copy:
        src: apache.conf
        dest: /etc/apache2/apache2.conf
      notify: Restart Apache

  handlers:
    - name: Restart Apache
      service:
        name: apache2
        state: restarted

### Explanation:

The copy task notifies the Restart Apache handler only if the file changes.
The handler block defines what should be done when notified (in this case, restart Apache).
If the file doesn’t change, the handler is skipped.

## Multiple notifications

You can have multiple tasks notify the same handler:

```yaml
- name: Update config 1
  copy:
    src: file1.conf
    dest: /etc/app/file1.conf
  notify: Restart App

- name: Update config 2
  copy:
    src: file2.conf
    dest: /etc/app/file2.conf
  notify: Restart App

handlers:
  - name: Restart App
    service:
      name: myapp
      state: restarted
```

The handler runs only once per play, no matter how many tasks notify it.

## Using Handlers with Tags

You can tag handlers just like tasks:

```yaml
handlers:
  - name: Restart nginx
    service:
      name: nginx
      state: restarted
    tags: restart
```

Run with

```bash
ansible-playbook site.yml --tags restart
```

## Best Practices

- Use handlers to control service restarts, reloads, reboots, etc.
- Name handlers clearly and consistently.
- Use notify only when changes should trigger a handler.
- Avoid putting logic inside handlers — they should be clean and focused.

## Summary

- Handlers are executed only when notified.
- Great for tasks like restarting services after config changes.
- Run at the end of a play after all tasks complete.
- Improve efficiency and reliability of your playbooks.
