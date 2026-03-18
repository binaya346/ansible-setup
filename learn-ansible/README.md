# 📚 Ansible Learning Path (Hands-on)

Welcome to the Ansible training! This course is designed to take you from a complete beginner to a confident automation engineer.

## 🛠 Lab Environment
We use a Docker-based lab environment.
- **Controller**: `ansible_controller` (Where you run commands)
- **Managed Nodes**: `node_01`, `node_02`

### Quick Start
1.  **Start Lab**: `docker-compose up -d`
2.  **Enter Controller**: `docker exec -it ansible_controller /bin/bash`
3.  **Go to Project**: `cd /home/ansible/project`

---

## 📖 Syllabus

| Topic | Description | Link |
| :--- | :--- | :--- |
| **01** | What is Ansible? Architecture | [Read Here](./01-introduction.md) |
| **02** | Installation & Lab Setup | [Read Here](./02-installation-lab.md) |
| **03** | Project Setup (Inventory, Config, Vars) | [Read Here](./03-project-setup.md) |
| **04** | Ad-hoc Commands | [Read Here](./04-ad-hoc-commands.md) |
| **05** | YAML Basics | [Read Here](./05-yaml-basics.md) |
| **06** | Playbooks, Modules, Handlers | [Read Here](./06-playbooks-modules.md) |
| **07** | Ansible Roles | [Read Here](./07-ansible-roles.md) |
| **08** | Server Configuration Example | [Read Here](./08-server-config.md) |

---

## 🚀 Hands-on Exercise
Once you've read through the chapters, try running the playground playbook:

```bash
# Inside the controller container:
cd /home/ansible/project
ansible-playbook 01_playground.yml
```

Explore the `01_playground.yml` file to see how it uses various modules!

---

## 📂 Project Structure
All working examples are integrated into the main project folder:
- **[01_playground.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/01_playground.yml)**: Basic modules demo.
- **[02_webserver_demo.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/02_webserver_demo.yml)**: Nginx setup with handlers.
- **[03_role_demo.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/03_role_demo.yml)**: Using Ansible Roles.
- **[04_variable_demo.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/04_variable_demo.yml)**: Advanced variables and logic.
