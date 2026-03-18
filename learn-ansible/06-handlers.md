# Lesson 06: Understanding Ansible Handlers

## 1. What are Handlers?

In Ansible, **Handlers** are special tasks that only run when they are "notified" by another task. 

Think of them as "Conditional Tasks" that respond to a change in the system.

### The Problem
Imagine you are deploying a new configuration file for Nginx.
- If the file is the **same** as before, you don't need to restart Nginx.
- If the file is **newly changed**, you MUST restart Nginx for the settings to take effect.

---

## 2. How Handlers Work (Notify + Handler)

A handler is like a "Subscriber." It waits for someone to tell it to "Wake up and do something."

### Step 1: The Notification
Inside your task, you use the `notify:` keyword. It must match the exact **name** of the handler.

```yaml
- name: Copy Nginx Config
  copy:
    src: nginx.conf
    dest: /etc/nginx/nginx.conf
  notify: Restart Nginx  <-- TELL THE HANDLER TO RUN IF THE FILE CHANGED
```

### Step 2: The Handler
In a separate section at the bottom of your playbook (the `handlers:` section), you define what to do.

```yaml
handlers:
  - name: Restart Nginx
    service:
      name: nginx
      state: restarted
```

---

## 3. Important Rules about Handlers

1.  **Only on Change**: A handler only runs if the notifying task reports a `changed` status. If the task says `ok` (nothing changed), the handler is skipped!
2.  **Runs at the End**: No matter where you notify it, handlers only run at the very end of all tasks in the play. This ensures that if you change 5 different config files, Nginx only restarts **once** at the finish.
3.  **Order Matters**: If multiple tasks notify the same handler, it still only runs once.

## 4. Real-World Scenario in our Project

Look at `project/02_webserver_demo.yml`. You will see task #03 notifying the handler:

```yaml
    - name: 03 - Copy base Nginx configuration
      copy:
        src: files/nginx.conf
        dest: /etc/nginx/nginx.conf
      notify: Restart Nginx

  handlers:
    - name: Restart Nginx
      service:
        name: "{{ web_package_name }}"
        state: restarted
```

### Exercise for Students:
1. Run the `02_webserver_demo.yml` playbook twice.
2. The **first time**, the config file is copy, and you will see "RUNNING HANDLER [Restart Nginx]" at the end.
3. The **second time**, the file already exists (no change), and you will notice that the handler is **not** triggered!
