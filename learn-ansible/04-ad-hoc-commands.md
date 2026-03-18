# 04 - Ansible Ad-hoc Commands

## What are Ad-hoc Commands?
Ad-hoc commands are quick, one-line tasks that you run from the command line without writing a full playbook.

- **How**: `ansible <group_or_host> -m <module_name> -a "<arguments>"`
- **Why**: Use them for quick, one-time tasks (e.g., restarting a service across 10 servers).
- **When**: When a full playbook is overkill for a simple task.

## Common Ad-hoc Examples

### 1. Ping (Check Connectivity)
Check if all hosts in the `webservers` group are reachable:
```bash
ansible webservers -m ping
```

### 2. Shell (Run Any Shell Command)
Check memory usage on all managed nodes:
```bash
ansible all -m shell -a "free -m"
```

### 3. Apt (Manage Packages)
Install `git` on all managed nodes:
```bash
ansible all -m apt -a "name=git state=present"
```

### 4. Service (Manage Services)
Restart the `nginx` service:
```bash
ansible webservers -m service -a "name=nginx state=restarted"
```

### 5. Copy (Copy Files)
Copy a local file to the remote nodes:
```bash
ansible all -m copy -a "src=/home/ansible/test.txt dest=/tmp/test.txt"
```

## Tips for Ad-hoc Commands:
- Use `all` to target every host in your inventory.
- Use the `-k` flag if you need to provide an SSH password.
- Ad-hoc commands are great for **exploration** before writing a permanent playbook.

---
[Next: YAML Basics](./05-yaml-basics.md)
