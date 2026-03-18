# 02 - Installing Ansible & Lab Setup

## Installing Ansible

### Method 1: Using pip (Recommended)
Since Ansible is written in Python, the easiest way to install it is through `pip`:
```bash
pip3 install ansible
```
This is how Ansible is installed in our lab environment (see `requirements.txt`).

### Method 2: OS-specific Package Managers
- **Ubuntu/Debian**: `sudo apt update && sudo apt install ansible -y`
- **macOS**: `brew install ansible`
- **RedHat/CentOS**: `sudo yum install ansible`

## Features & Limitations

### Features:
- **Modular**: Over 3000 modules for everything from managing users to cloud resources.
- **Extensible**: You can write your own modules in any language.
- **Low Overhead**: No background processes or agents running on managed nodes.

### Limitations:
- **No GUI**: Primarily CLI-based (Ansible Semaphore or AWX/Tower provide GUIs).
- **Steep Learning Curve for Complex Tasks**: While basics are easy, advanced orchestration requires deep knowledge.
- **SSH Latency**: For very large fleets (thousands of nodes), SSH performance can be a bottleneck.

## Setting up Lab Environment for Ansible

Our lab uses **Docker Compose** to simulate a real-world network.

### Lab Architecture:
- `ansible_controller`: Ubuntu-based container where we run Ansible.
- `node_01`, `node_02`: Target containers managed by the controller.

### To start the lab:
1.  **Build and Start**:
    ```bash
    docker-compose up -d --build
    ```
2.  **Access Controller**:
    ```bash
    docker exec -it ansible_controller /bin/bash
    ```

### Why use Docker for Lab?
Docker allows us to quickly spin up multiple "servers" on a single laptop without the overhead of Virtual Machines.

---
[Next: Project Setup: Inventory, Configurations & Variables](./03-project-setup.md)
