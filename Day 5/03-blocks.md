# Blocks in Ansible

Blocks in Ansible allow you to group tasks together and apply directives (`when`, `become`, `tags`, etc.) to all tasks in the block. They are also useful for implementing error handling with `rescue` and `always`.

---

## 1. Basic Block Structure

```yaml
- name: Block of tasks
  block:
    - name: Task 1
      debug:
        msg: "This is the first task in the block"

    - name: Task 2
      debug:
        msg: "This is the second task in the block"
```

## 2. Applying Directives to the Whole Block

```yaml
- name: Block with become and when
  block:
    - name: Install a package
      apt:
        name: git
        state: present
  become: true
  when: ansible_facts['os_family'] == "Debian"
```

 The `become` and `when` are applied to every task inside the block.

## 3. Using `rescue` and `always`

Blocks allow error handling using rescue and always, similar to try-catch-finally in programming.

```yaml
- name: Block with error handling
  block:
    - name: Risky command
      command: /bin/false
  rescue:
    - name: Handle failure
      debug:
        msg: "The risky command failed, but we handled it."
  always:
    - name: Always runs
      debug:
        msg: "This will always run, regardless of success or failure."
```

## 4. Nested Blocks

Blocks can be nested for more complex structures.

```yaml
- name: Outer block
  block:
    - name: Inner block
      block:
        - name: Inner task
          debug:
            msg: "Inside nested block"
```

## 5. Tags on Blocks

```yaml
- name: Tagged block
  block:
    - name: Task A
      debug:
        msg: "Task A running"
    - name: Task B
      debug:
        msg: "Task B running"
  tags: [my_block]
```

Then you can run with:

```bash
ansible-playbook playbook.yml --tags my_block
```

## Summary

| Feature | Description |
|--|--|
| `block` | Groups multiple tasks |
| `rescue`| Tasks to run if the block fails |
| `always` | Tasks that run regardless of block success/failure |
| `tags` | Apply tags to multiple tasks |
| `when`, `become` | Apply conditions or privilege escalation to all tasks in the block |

Use blocks for better readability, reusability, and error management in playbooks.
