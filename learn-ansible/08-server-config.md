# 08 - Server Configuration through Ansible

## Real-world Example: Setting up a Web Server
In this chapter, we'll see how to combine everything you've learned to configure a web server from scratch.

### 1. Update the Inventory
Make sure your `hosts.yml` has the correct IP addresses for your web servers.

### 2. Create the Playbook
Create a file called `setup_webserver.yml`:
```yaml
---
- name: Setup Webserver
  hosts: webservers
  become: yes
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
    - name: Install Nginx
      apt:
        name: nginx
        state: present
    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: yes
    - name: Copy custom index.html
      copy:
        src: files/index.html
        dest: /var/www/html/index.html
```

### 3. Run the Playbook
Run the playbook from the control node:
```bash
ansible-playbook setup_webserver.yml
```

### 4. Verify the Configuration
You can verify the configuration by checking if Nginx is running and serving your custom index.html:
```bash
curl http://<server_ip>
```

## Putting it all Together: Working Example

We have consolidated all the concepts from this course into a single, ready-to-run playbook that configures a complete Nginx web server with a custom welcome page.

### Full Example Playbook
- **Playbook**: [02_webserver_demo.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/02_webserver_demo.yml)
- **Status Check**: [01_playground.yml](file:///Users/binayadai/Documents/techaxis/ansible-setup/project/01_playground.yml)

### Why this approach?
- **Inventory**: To target your servers.
- **Variables**: To store dynamic values (like the website source).
- **Tasks**: To perform the actual work (installing Nginx, copying files).
- **Handlers**: To restart Nginx when the configuration changes.
- **Roles**: To organize your playbooks for better maintainability and reusability.

### When to use this?
Every time you need to set up a new server from scratch, you should use a base playbook like this one to ensure consistency and speed.

---
[Back to Main Menu](../README.md)
