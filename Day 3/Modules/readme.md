# Ansible Modules Overview

Ansible modules are the **building blocks** of automation in playbooks. They define what action should be performed on the target host(s).

Below is a categorized summary of commonly used Ansible module types:

---

## 1. Core System Modules

| Category     | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| Command      | Run shell commands (non-idempotent)                     | `command`, `shell`, `raw`   |
| File         | Manage files and directories                            | `file`, `copy`, `template`, `stat` |
| User         | Manage users and groups                                 | `user`, `group`, `authorized_key` |
| Cron         | Schedule cron jobs                                      | `cron`                      |
| Service      | Start/stop/manage system services                       | `service`, `systemd`        |
| Package      | Install/remove packages using OS package managers       | `apt`, `yum`, `dnf`, `package` |

---

## 2. Networking & Firewall

| Category     | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| Network      | Manage network interfaces, IPs, routes                  | `nmcli`, `interfaces`, `ios_interface` |
| Firewall     | Manage firewall rules                                   | `firewalld`, `ufw`, `iptables`         |

---

## 3. Cloud Modules

| Provider     | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| AWS          | Manage AWS infrastructure                              | `ec2`, `s3_bucket`, `iam_user`, `route53` |
| Azure        | Manage Azure resources                                  | `azure_rm_resourcegroup`, `azure_rm_virtualmachine` |
| GCP          | Manage Google Cloud resources                           | `gcp_compute_instance`, `gcp_storage_bucket` |

---

## 4. Security & Crypto

| Category     | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| Crypto       | Manage certificates and keys                            | `openssl_certificate`, `win_certificate_store` |
| Secrets      | Retrieve secrets from vaults or secure stores           | `ansible.builtin.debug`, `community.hashi_vault.hashi_vault` |

---

## 5. Database Modules

| DB Type      | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| MySQL        | Manage MySQL users, databases, permissions              | `mysql_db`, `mysql_user`    |
| PostgreSQL   | Manage PostgreSQL roles and databases                   | `postgresql_db`, `postgresql_user` |
| MongoDB      | Limited community modules available                     | Community-maintained        |

---

## 6. Clustering & Load Balancing

| Tool         | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| HAProxy      | Configure HAProxy load balancer                         | `haproxy` (via templates)   |
| Kubernetes   | Manage k8s objects and clusters                         | `k8s`, `helm`               |
| Docker       | Manage Docker containers and images                     | `docker_container`, `docker_image` |

---

## 7. Archive, Compression & Deployment

| Tool         | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| Archive      | Compress and extract files                              | `unarchive`, `archive`      |
| Git          | Manage Git repositories                                 | `git`                       |
| Deploy       | Push app builds using tools                             | `copy`, `rsync`, `synchronize` |

---

## 8. Windows Modules

| Category     | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| Win User     | Manage Windows users and groups                         | `win_user`, `win_group`     |
| Win Package  | Install or uninstall Windows software                   | `win_package`, `win_chocolatey` |
| Win Service  | Manage Windows services                                 | `win_service`               |
| Win Registry | Edit registry entries                                   | `win_regedit`, `win_reg_stat` |

---

## 9. Monitoring & Logs

| Tool         | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| Log Mgmt     | Read/write log entries                                  | `lineinfile`, `slurp`, `lookup` |
| Monitoring   | Send alerts, interact with monitoring APIs              | `prometheus`, `nagios`, `datadog_monitor` |

---

## 10. Miscellaneous Modules

| Category     | Description                                             | Example Modules             |
|--------------|---------------------------------------------------------|------------------------------|
| Setup        | Gather system facts and metadata                        | `setup`                     |
| Assert       | Perform logical checks in playbooks                     | `assert`, `fail`, `debug`   |
| Wait         | Wait for host, port, or file before continuing          | `wait_for`, `pause`         |
| Notification | Send messages to systems or users                       | `slack`, `mail`, `telegram` |

---

## Best Practices

- Use **idempotent modules** to ensure repeatability.
- Avoid `shell` or `command` when a built-in module exists.
- Explore the [Ansible Docs](https://docs.ansible.com/ansible/latest/collections/index.html) for a full list.

---

## 📎 Useful Links

- [Ansible Built-in Modules](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html)
- [Community Collections on Galaxy](https://galaxy.ansible.com/)

---
