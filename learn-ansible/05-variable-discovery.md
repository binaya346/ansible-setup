# Lesson 05: How Ansible Finds Your Variables

A common question for beginners is: *"How does the role know where `base_packages` or `custom_welcome_message` is defined?"*

Ansible uses an automatic discovery mechanism based on the **Project Structure**.

## 1. The Variable Discovery Rules

When you run:
`ansible-playbook -i inventory/hosts.yml 03_role_demo.yml`

Three things happen automatically behind the scenes:

### 1. Where do we define the nodes? (Targeting)
Inside your playbook (`03_role_demo.yml`), you will see this line:
```yaml
- name: Role-based Playbook Demo
  hosts: all  <-- THIS IS THE TARGET
```
The `hosts: all` tells Ansible: *"Look at the inventory file provided on the command line, and run this on EVERY host found inside it."*

- If you change it to `hosts: webservers`, it will only run on nodes listed under that group in `hosts.yml`.
- This is how Ansible knows **which** nodes to talk to.

### 2. How are the variables "pulled in"? (Merging)
When you specify the inventory (`-i inventory/hosts.yml`), Ansible reads it and builds a list of hosts. For **each host** in that list, it immediately asks:
- *"Does this host belong to any groups (like 'webservers')? If yes, go find `group_vars/webservers.yml`."*
- *"Is there a specific file for this host? Go find `host_vars/node_01.yml`."*
- *"Is there an `all.yml`? Every host needs those defaults!"*

Ansible then **merges** all these files into one big list of variables for that specific host right before it starts the tasks.

### Discovery Scopes (The "Search Order"):
Ansible is smart! It doesn't just look in one place; it checks **both** of these locations:

1.  **The Playbook Directory**: (Where your `.yml` playbook file lives)
2.  **The Inventory Directory**: (Where your `hosts.yml` file lives)

### Why it works in our project:
In our setup:
- Your playbook is at: `project/03_role_demo.yml`
- Your variables are at: `project/group_vars/`

Since the **Playbook** and the **Variables** are in the same folder (`project/`), Ansible finds them immediately! It doesn't matter that they aren't inside the `inventory/` folder, because the Playbook directory is also a valid search location.

---

## 2. Real-World Scenario: The `common` Role

Let's look at how the `common` role in `roles/common/tasks/main.yml` behaves differently for different nodes.

### Picking up `base_packages` (Global)
- Inside `group_vars/all.yml`, we defined `base_packages`.
- Since every host is part of the `all` group, this variable is loaded for **every** host.
- When the `common` role runs on `node_01` or `node_02`, it sees `{{ base_packages }}` and installs the list we defined.

### Picking up `custom_welcome_message` (Host-Specific)
- Inside `host_vars/node_01.yml`, we defined a unique message.
- Inside `host_vars/node_02.yml`, we defined a different message.
- **Scenario**: You want your primary server to say "Primary" and your backup to say "Secondary" when someone logs in.
- When Ansible runs the `common` role on `node_01`, it looks into `host_vars/node_01.yml` and finds the specific message. It **ignores** `node_02.yml` for this host.

---

## 3. Running Against Different Variables

What if you want to override a variable temporarily without changing any files? You can use **Extra Vars**.

### Scenario: Emergency Package Install
If you need to install a specific package just this once on all nodes:
```bash
ansible-playbook -i inventory/hosts.yml project/03_role_demo.yml -e "base_packages=['htop', 'git']"
```
The `-e` (extra vars) has the **absolute highest priority** and will override everything in `all.yml`, `group_vars`, and `host_vars`.

### Scenario: Test a Different Port
To test `node_01` on a different port without editing the file:
```bash
ansible-playbook -i inventory/hosts.yml project/05_vars_hierarchy_demo.yml -e "http_port=9999" --limit node_01
```

---

## 4. Filtering and Limiting Execution

Sometimes you have 100 servers in your inventory, but you only want to run your playbook on **one** of them. You have two main ways to do this:

### Option A: The `--limit` flag (Recommended)
You don't need to change your playbook! Just add the `--limit` (or `-l`) flag to your command:

```bash
# Run only on node_01
ansible-playbook -i inventory/hosts.yml project/03_role_demo.yml --limit node_01
```

- You can also limit to a group: `--limit webservers`
- This is the safest way to "test" a change on one node before rolling it out to the whole fleet.

### Option B: Changing the Playbook
You can edit the `hosts:` line inside your `.yml` file:
```yaml
- name: Role-based Playbook Demo
  hosts: node_01  # Changed from 'all' to a specific node
  roles:
    - common
```

---

## Summary for Students
- `all.yml` = The foundation (Global defaults).
- `group_vars/` = The specialized layer (Web, DB, etc).
- `host_vars/` = The unique layer (One-off overrides).
- `-e` flag = The emergency override (Command line).
- `--limit` flag = The surgical tool (Targeting one node).
