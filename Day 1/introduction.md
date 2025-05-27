# 📘 Day 1 - Getting Started with Ansible
 
Today’s focus: Understanding what Ansible is, how it compares with other tools, and how to get started with basic usage.

---

## 📌 Topics Covered

### ✅ 1. Overview of Ansible

**Ansible** is an open-source automation tool used for:
- Configuration management
- Application deployment
- Task automation (cron, package installs, user management)
- Cloud provisioning (e.g., Azure, AWS)

**Advantages:**
- Agentless (uses SSH/WinRM)
- Human-readable YAML syntax
- Easy to learn
- Scales from small setups to large infrastructures
- Idempotent (no repeated unnecessary changes)

---

### 🔁 2. Ansible vs Shell & Python Scripting

| Feature            | Shell Script     | Python Script        | Ansible                    |
|--------------------|------------------|-----------------------|----------------------------|
| Ease of Use        | Medium            | Medium-High           | High (YAML-based)          |
| Reusability        | Low               | Medium                | High (roles, tasks)        |
| Idempotency        | No                | With effort           | Yes (built-in)             |
| Remote Execution   | Manual (via SSH) | Paramiko/Fabric needed| Built-in SSH agentless     |
| Readability        | Depends           | Good                  | Excellent (declarative)    |

---

### 🧰 3. Ansible vs Other Tools

| Tool      | Agentless | Language | Cloud Native Support | Learning Curve |
|-----------|-----------|----------|----------------------|----------------|
| **Ansible**  | ✅        | YAML     | Azure, AWS, GCP       | Low             |
| Puppet     | ❌        | Ruby     | Medium                | High            |
| Chef       | ❌        | Ruby     | Medium                | High            |
| SaltStack  | ✅        | YAML/Python | High              | Medium          |

🔎 *Ansible is preferred for simplicity, especially in teams with mixed experience levels.*

---

### ⚙️ 4. Terraform vs Ansible

| Feature                | Terraform          | Ansible                |
|------------------------|--------------------|------------------------|
| Purpose                | Infrastructure as Code | Configuration Management |
| Language               | HCL                | YAML                   |
| Cloud Provisioning     | ✅                 | Limited                |
| Configuration Tasks    | ❌ (external tools)| ✅                     |
| Idempotency            | ✅                 | ✅                     |
| Use Together?          | ✅ Yes             | ✅ Yes                 |

📌 **Use Terraform to provision infrastructure (VMs, networks)**  
📌 **Use Ansible to configure it (install packages, set permissions, etc.)**

---








