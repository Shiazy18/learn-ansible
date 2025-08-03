# Dynamic Inventory in Ansible

Ansible uses an inventory file to know which hosts to manage. While a static inventory lists hosts manually, **dynamic inventory** fetches host information from an external source like cloud providers (AWS, Azure, etc.).

---

## 1. What is Dynamic Inventory?

Dynamic inventory allows Ansible to query real-time infrastructure data instead of relying on a static list of IPs or hostnames.

---

## 2. Use Cases

- Cloud environments (AWS, Azure, GCP)
- Kubernetes clusters
- CMDB integrations
- Docker containers

---

## 3. Structure of a Dynamic Inventory Script

A dynamic inventory script should:

- Output JSON
- Accept `--list` and `--host <hostname>` arguments

---

## 4. Example: Basic Custom Dynamic Inventory Script

### `inventory.py`

```python
#!/usr/bin/env python3
import json
import sys

inventory = {
    "web": {
        "hosts": ["web1.example.com", "web2.example.com"],
        "vars": {
            "ansible_user": "ubuntu"
        }
    },
    "_meta": {
        "hostvars": {
            "web1.example.com": {"env": "prod"},
            "web2.example.com": {"env": "staging"}
        }
    }
}

if __name__ == "__main__":
    if len(sys.argv) == 2 and sys.argv[1] == "--list":
        print(json.dumps(inventory))
    elif len(sys.argv) == 3 and sys.argv[1] == "--host":
        host = sys.argv[2]
        print(json.dumps(inventory["_meta"]["hostvars"].get(host, {})))
    else:
        print("Usage: inventory.py --list or --host <hostname>")
```

 Don't forget to chmod +x inventory.py before using it.

## 5. Using Dynamic Inventory in a Playbook

```bash
ansible-playbook -i inventory.py playbook.yml
```

## 6. Example with AWS (using ansible-inventory plugin)

Install the AWS inventory plugin:

```bash
pip install boto boto3
```

Create an inventory config file:
`aws_ec2.yml`

```yaml
plugin: aws_ec2
regions:
  - us-west-2
filters:
  tag:Role: web
hostnames:
  - public-ip-address
```

Then run:

```bash
 ansible-inventory -i aws_ec2.yml --list
```

## 7. Benefits

| Advantage | Description                              |
| --------- | ---------------------------------------- |
| Real-time | Automatically reflects infra changes     |
| Scalable  | Supports hundreds/thousands of instances |
| Flexible  | Easily integrates with cloud providers   |

