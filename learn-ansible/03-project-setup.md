# 03 - Project Setup: Inventory, Configurations & Variables

## Ansible Inventory

The **Inventory** is a list of all hosts Managed by Ansible. You can group hosts for targeted management.

- **File Path in Lab**: `project/inventory/hosts.yml`
- **What it does**: Tells Ansible *where* to go.

### Example (YAML format):
```yaml
webservers:
  hosts:
    node_01:
      ansible_host: 10.99.0.11
    node_02:
      ansible_host: 10.99.0.12
```

## Ansible Configuration (`ansible.cfg`)

The `ansible.cfg` file controls Ansible's behavior globally for a project.

- **File Path in Lab**: `project/ansible.cfg`
- **Why it's important**: You can set default users, point to the inventory, and toggle security settings like `host_key_checking`.

### Key Settings:
- `inventory`: Path to your hosts file.
- `remote_user`: The user Ansible uses to SSH into nodes.
- `become`: Set to `True` if you want to run tasks as `root` (sudo).

## Variables in Ansible

Variables are the "data" that make your playbooks dynamic. Without them, you'd have to hard-code everything.

### 1. Group Variables (`group_vars/`)
**What**: Variables that apply to a group of hosts.
**Significance**: This is how you manage multiple environments (e.g., `prod` vs `dev`). If you have 50 web servers, you don't want to change the Nginx version 50 times. You change it once in `group_vars/webservers.yml`.
- **In Lab**: See [group_vars/all.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/group_vars/all.yml) for packages we install on *every* machine.

### 2. Host Variables (`host_vars/`)
**What**: Variables unique to a specific host.
**Significance**: Use these for things that *must* be different, like a unique IP address, a specific database ID, or a custom welcome message for just one server.
- **In Lab**: See [host_vars/node_01.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/host_vars/node_01.yml) for a message only for node 01.

### Why keep these for the course?
- **Variable Precedence**: We need to learn that "specific beats general" (Host vars override Group vars).
- **Separation of Concerns**: It teaches us to keep "logic" (playbooks) separate from "configuration" (variables).

---
[Next: Ansible Ad-hoc Commands](./04-ad-hoc-commands.md)
