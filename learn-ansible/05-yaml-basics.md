# 05 - YAML Basics

## What is YAML?
YAML (YAML Ain't Markup Language) is a human-readable data serialization language. Ansible uses YAML for its playbooks because it's clean and easy to read.

- **Why**: Ansible needs a structured way to define tasks, and YAML is the industry standard for configuration.
- **When**: Every time you write an Ansible playbook, you are writing YAML.

## Key YAML Rules:
1.  **Indentation Matters**: Use **spaces**, NOT tabs. Usually 2 spaces per level.
2.  **Key-Value Pairs**: `key: value` (note the space after the colon).
3.  **Lists**: Start with a dash `-`.
4.  **Dictionaries**: A collection of key-value pairs.
5.  **Booleans**: `true`, `false`, `yes`, `no`.
6.  **Strings**: Quotes are optional unless the string contains special characters like `:` or `*`.

## Example Breakdown:

```yaml
---
# This is a comment
- name: Configure Webserver
  hosts: webservers
  vars:
    http_port: 80
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present
```

### Let's analyze:
- `---`: Optional, but marks the start of a YAML document.
- `- name: ...`: The start of a list item (a Play).
- `tasks:`: A key whose value is a list of tasks.
- `apt:`: A dictionary representing the `apt` module's parameters.

## Common Pitfalls:
- **Mixing tabs and spaces**: Ansible will throw an error.
- **Missing space after colon**: `name:git` is WRONG. `name: git` is CORRECT.
- **Incorrect indentation**: A sub-item must be further indented than its parent.

---
[Next: Writing Ansible Playbooks & Modules](./06-playbooks-modules.md)
