# Ansible Vault

Ansible Vault is a feature that allows you to **secure sensitive data** such as passwords, API keys, or any confidential information by encrypting YAML files.

---

## Why Use Vault?

- Protect credentials, tokens, SSH keys, and more.
- Keep secrets safe when storing playbooks in version control.
- Use encrypted files directly in playbooks without manual decryption.

---

## Basic Commands

### Encrypt a file

```bash
ansible-vault encrypt secrets.yml
```

### Decrypt a file

```bash
ansible-vault decrypt secrets.yml
```

### Edit an encrypted file

```bash
ansible-vault edit secrets.yml
```

### Re-key (change the password)

```bash
ansible-vault rekey secrets.yml
```

---

## Using Vault in Playbooks

If you have an encrypted file with sensitive variables:

```yaml
# secrets.yml (encrypted)
db_user: admin
db_pass: SuperSecret123
```

You can include it in your playbook like this:

```yaml
---
- name: Using vault-encrypted secrets
  hosts: web
  vars_files:
    - secrets.yml
  tasks:
    - name: Show DB user
      debug:
        msg: "DB User is {{ db_user }}"
```

Then run the playbook with:

```bash
ansible-playbook playbook.yml --ask-vault-pass
```

Or use a vault password file:

```bash
ansible-playbook playbook.yml --vault-password-file ~/.vault_pass.txt
```

---

## Creating Encrypted Variables Inline

You can encrypt only specific values using:

```bash
ansible-vault encrypt_string 'MyPassword123' --name 'db_pass'
```

This outputs:

```yaml
db_pass: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          6666653561643533...
```

Use this directly in your playbooks or vars files.

---

## Best Practices

- Never hardcode secrets in plain text.
- Use `--vault-password-file` in CI/CD pipelines for automation.
- Organize secrets into separate files (`vault_vars.yml`) per environment.
- Consider using tools like Ansible Tower, AWX, or HashiCorp Vault for more advanced secret management.

---

## Summary

| Task               | Command/Usage                                    |
|--------------------|--------------------------------------------------|
| Encrypt file       | `ansible-vault encrypt <filename>`              |
| Decrypt file       | `ansible-vault decrypt <filename>`              |
| Edit file          | `ansible-vault edit <filename>`                 |
| Use in playbook    | Add to `vars_files`                             |
| Run with prompt    | `--ask-vault-pass`                              |
| Run with file      | `--vault-password-file <path>`                  |

---

**Ansible Vault** is an essential tool for secure automation. Practice encrypting secrets, integrating them into your playbooks, and rotating vault passwords regularly.
