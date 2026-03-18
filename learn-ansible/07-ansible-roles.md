# 07 - Writing Ansible Roles

## What are Ansible Roles?
Roles are a way to organize your playbooks into a reusable and modular directory structure.

- **How**: `ansible-galaxy init roles/<role_name>`
- **Why**: Use them to share code between different playbooks and projects.
- **When**: When your playbooks become too long or when you need to reuse the same logic across multiple projects.

## Role Directory Structure:
A typical role looks like this:
```text
roles/
  common/               # Name of the role
    tasks/              # Main list of tasks
      main.yml
    handlers/           # Handlers for this role
      main.yml
    templates/          # Templates used by this role
      ntp.conf.j2
    files/              # Files to be copied
      id_rsa.pub
    vars/               # Variables for this role
      main.yml
    defaults/           # Default variables (lowest priority)
      main.yml
    meta/               # Metadata about the role (dependencies)
      main.yml
```

## Roles: Direct Example

We have prepared a working role for you to explore:
- **Role Directory**: [roles/common](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/roles/common)
- **Role Tasks**: [tasks/main.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/roles/common/tasks/main.yml)
- **Demo Playbook**: [03_role_demo.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/03_role_demo.yml)

### Why use Roles?
1.  **Maintainability**: Easier to find and edit specific parts of your automation.
**How**: Group related tasks, variables, and files into a single directory.
**Why**: Keeps your project organized as it scales.

2.  **Reusability**: Share common roles (like `common`, `webserver`, `dbserver`) across different teams.
**When**: When you find yourself copy-pasting code between different playbooks.

3.  **Encapsulation**: Hide complex logic inside a simple role call.
**How**: Move complex tasks into the role's `tasks/main.yml` and only expose global variables in `defaults/main.yml`.

---
[Next: Server Configuration through Ansible](./08-server-config.md)
