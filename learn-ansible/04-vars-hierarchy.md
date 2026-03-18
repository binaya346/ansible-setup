# Lesson 04: Understanding Ansible Variable Hierarchy

In this lesson, we will explore how Ansible manages variables across different scopes: **Global**, **Group**, and **Host**. 

## 1. Why use separate variable files?

Keeping variables separate from playbooks is a best practice. It allows you to:
- **Reuse Playbooks:** The same playbook can be used for different environments (Dev, Staging, Prod) just by changing the variable files.
- **Maintainability:** Easier to update a single value in one place than searching through multiple playbooks.
- **Clarity:** It's immediately clear what configurations apply to which servers.

## 2. The Hierarchy (Variable Precedence)

Ansible follows a specific order when merging variables. If the same variable name is defined in multiple places, the one with the "highest priority" wins.

The general order from **Lowest to Highest** priority is:
1.  **Global Vars (`group_vars/all.yml`)**: Shared by every host.
2.  **Group Vars (`group_vars/webservers.yml`)**: Shared by hosts in a specific group.
3.  **Host Vars (`host_vars/node_01.yml`)**: Specific to a single host.
4.  **Playbook Vars (`vars:` section)**: Defined directly inside your `.yml` playbook file.
5.  **Extra Vars (`-e` flag)**: Defined on the command line (The ultimate winner).

### Why do Playbook Vars win over Host Vars?
Ansible assumes that if you took the time to write a variable **directly into a specific playbook**, it's because you want that playbook to behave in a very specific way, overriding whatever generic "host-level" settings might exist elsewhere.

## 3. Real-World Examples in this Project

We have set up the following structured examples for you to explore:

- `group_vars/all.yml`: Contains global settings like `admin_email` and `base_packages`.
- `group_vars/webservers.yml`: Contains web-specific variables like `http_port` and `doc_root`.
- `host_vars/node_01.yml`: Contains an override for `http_port` (set to 8080) and a custom `welcome_message`.

### How to Run and Verify

To see how these variables are merged by Ansible without running a playbook, you can use the `ansible-inventory` tool:

```bash
# View the consolidated variables for node_01
ansible-inventory -i inventory/hosts.yml --host node_01

# View the consolidated variables for node_02
ansible-inventory -i inventory/hosts.yml --host node_02
```

Compare the `precedence_test` and `http_port` values for both nodes to see the hierarchy in action!

## 4. Practical Demonstration

We have created a demonstration playbook: `project/05_vars_hierarchy_demo.yml`.

To run it:
```bash
ansible-playbook -i inventory/hosts.yml project/05_vars_hierarchy_demo.yml
```

Pay attention to the output for each host. You will notice that `node_01` uses its own specific `http_port`, while `node_02` inherits the group-level `http_port`.
