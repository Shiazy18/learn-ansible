# Error Handling in Ansible

Error handling in Ansible is critical to ensuring your automation behaves reliably and predictably. This includes stopping on failure, skipping tasks, retrying operations, and gracefully handling errors.

---

## 1. `ignore_errors`

Use `ignore_errors: yes` when you want a task failure to not stop the playbook execution.

```yaml
- name: Try to stop a service that may not exist
  ansible.builtin.service:
    name: nonexistent_service
    state: stopped
  ignore_errors: yes
```

## 2. `failed_when`

Customize the failure condition. Useful when the default success/failure behavior of a module isn’t sufficient.

```yaml
- name: Check a command output and fail only on specific output
  command: /usr/bin/my_app --check
  register: result
  failed_when: "'CRITICAL' in result.stdout"
```

## 3. `rescue` and `always`   

Use block with `rescue` and `always` for try-catch-finally-like behavior.

```yaml
- name: Block example with rescue and always
  block:
    - name: Run a risky command
      command: /bin/false
  rescue:
    - name: Handle the failure
      debug:
        msg: "Something went wrong, but we handled it."
  always:
    - name: Always run this
      debug:
        msg: "This task always runs, success or failure."
```

## 4. `when` for Conditional Execution

Skip tasks dynamically if certain conditions are met, avoiding errors.

```yaml
- name: Only run if user exists
  user:
    name: testuser
    state: absent
  when: ansible_facts['user_id'] is defined
```

## 5. `retries`, `delay`, and `until`

Retry a task if it fails, useful for transient errors.

```yaml
- name: Retry until service is up
  uri:
    url: http://localhost:8080/health
    status_code: 200
  register: result
  until: result.status == 200
  retries: 5
  delay: 10
```

## 6. `check_mode` and `changed_when`

Control task behavior in dry run and customize when a task is considered changed.

```yaml
- name: Dry-run supported task
  file:
    path: /tmp/test
    state: touch
  check_mode: yes

- name: Custom changed logic
  command: some_command
  register: result
  changed_when: "'updated' in result.stdout"
```

## Summary

| Feature | Purpose    |  
|----------|----------- |
| ignore_errors       | Continue on failure |
|    failed_when    | Customize what is considered a failure |
| block        | Group tasks with try (block), catch (rescue), and finally (always) |
|retries/until        | Retry task until a condition is met |
|   changed_when     |  Define what makes a task “changed” |
| check_mode | check_mode |

---

Proper error handling ensures your automation is resilient and easier to troubleshoot.
