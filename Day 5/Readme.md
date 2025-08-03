# Day 5: Ansible - Templating, Error Handling, and Dynamic Inventories

Welcome to **Day 5** of our Ansible journey! Today, we'll explore advanced capabilities that make your automation more flexible, intelligent, and production-ready.

---

## Topics Covered

### 1. Jinja2 Templating

Learn how to use Jinja2 to render dynamic content in configuration files, scripts, and variables.

### 2. Error Handling

Handle task failures gracefully using:

- `ignore_errors`
- `failed_when`
- `rescue` & `always` blocks

### 3. Blocks

Group related tasks together for better structure, and apply common directives like `when`, `tags`, etc.

### 4. Dynamic Inventories

Use dynamic sources like cloud APIs or scripts to populate the inventory dynamically instead of static INI/YAML files.

---

## What's covered

- Create templated config files with Jinja2
- Use control flow in templates (`if`, `for`, filters)
- Handle failed tasks without stopping the play
- Use blocks with `rescue` and `always`
- Integrate a Python or Bash script as an inventory plugin
- Pull inventory from cloud (AWS, Azure, etc.)

---

## Sample Playbook Highlights

- Templating an Nginx config  
- Gracefully skipping failed services  
- Using a Python script to generate inventory  
- Grouped task execution with recovery

---

## Files in This Day
[01-Roles.md](./01-Roles.md)

| File Name               | Description                                |
|------------------------|--------------------------------------------|
| [Jinja2 Template](./01-jinja2_templating.md)   | Basics and examples of using Jinja2        |
| [Error Handling](./02-error_handling.md)       | Strategies to handle errors effectively     |
| [Blocks](./03-blocks.md)                       | Grouping tasks and using rescue/always     |
| [Dynamic Inventory](./04-dynamic_inventory.md) | Creating and using dynamic inventories      |

---

## 🚀 Outcome

By the end of Day 5, you'll be able to:

- Dynamically generate configs and scripts with templates
- Write resilient playbooks that don’t crash on every error
- Manage inventory for large, cloud-based infrastructure setups

> 🎯 **Level up your automation game by making it dynamic, reusable, and resilient!**

---

🔜 Ready? Let’s begin with [jinja2_templating.md](jinja2_templating.md) 🔧
