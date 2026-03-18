# 01 - What is Ansible? & Architecture

## What is Ansible?
Ansible is an open-source IT automation engine that automates cloud provisioning, configuration management, application deployment, intra-service orchestration, and many other IT needs.

### Why Ansible?
- **Simple**: Ansible uses human-readable YAML for playbooks. No special coding skills are needed.
- **Agentless**: You don't need to install any agent software on the managed nodes. It uses SSH (for Linux) or WinRM (for Windows).
- **Idempotent**: This is a key concept. It means you can run the same operation multiple times, and it will only make changes if they are necessary to reach the desired state.
- **Powerful**: It can model even highly complex IT workflows.

## Ansible Architecture

Ansible's architecture consists of two main types of machines:

1.  **Control Node**: The machine where Ansible is installed. This is where you run commands and playbooks.
2.  **Managed Nodes**: The remote systems (servers, network devices, etc.) that Ansible manages.

### How it works:
1.  **Inventory**: Ansible reads a list of managed nodes from an inventory file.
2.  **Modules**: Ansible pushes small programs called "Ansible modules" to the managed nodes.
3.  **Execution**: These modules are executed on the managed nodes to perform tasks.
4.  **Removal**: Once the task is done, the modules are removed.

### When to use it?
- When you have more than a few servers to manage.
- When you want to ensure consistent configuration across environments.
- When you want to automate repetitive tasks like system updates, user management, or app deployments.

---
[Next: Installing Ansible & Lab Setup](./02-installation-lab.md)
