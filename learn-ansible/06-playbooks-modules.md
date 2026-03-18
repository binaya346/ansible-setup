# 06 - Writing Ansible Playbooks & Modules

## What is a Playbook?
A Playbook is a file that contains a series of "plays" to be executed on a group of hosts.

- **How**: `ansible-playbook <playbook_name>.yml`
- **Why**: Use them for repeatable, complex tasks.
- **When**: Every time you want to automate a configuration or deployment.

## Core Components:
1.  **Hosts**: Which servers should this play run on?
2.  **Vars**: Variables specific to this play.
3.  **Tasks**: A list of actions to perform.
4.  **Handlers**: Special tasks that run only when notified by another task (e.g., restart Nginx after a config change).

## Essential Modules:
- `apt`: Manages packages on Debian/Ubuntu.
- `service`: Manages system services (start, stop, restart).
- `copy`: Copies files from the control node to managed nodes.
- `template`: Similar to copy, but allows you to use Jinja2 variables.
- `file`: Manages file permissions, ownership, and directories.
- `lineinfile`: Ensures a specific line is in a file.

## Decisions and Handlers: Direct Example

Let's look at the actual working playbook for this concept.

- **Playbook**: [02_webserver_demo.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/02_webserver_demo.yml)
- **Resource (Config)**: [nginx.conf](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/files/nginx.conf)
- **Resource (Template)**: [index.html.j2](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/files/index.html.j2)

### 1. Conditionals (`when`)
**What**: A way to skip tasks based on specific criteria.
**How**: Use the `when` keyword at the end of a task.
**Why**: Different servers might need different configurations (e.g., Ubuntu vs. CentOS).
**When**: To handle heterogeneous environments or specific system states.

### 2. Handlers (`notify`)
**What**: Tasks that run only when "notified" by another task that made a change.
**How**: Use `notify` in a task and define the task under `handlers`.
**Why**: To avoid unnecessary service restarts (e.g., only restart Nginx if its config actually changed).
**When**: For any configuration change that requires a service reload or restart.

### 3. Templates (`template`)
**What**: Files that contain Jinja2 variables which are replaced by their values during execution.
**How**: Use the `template` module with a `.j2` source file.
**Why**: To create dynamic configuration files tailored to each specific host.
**When**: When you need your config files to include hostnames, IP addresses, or custom variables.

---
[Next: Writing Ansible Roles](./07-ansible-roles.md)
