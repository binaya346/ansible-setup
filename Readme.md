# Running project
`docker-compose up -d --build`
The `--build` flag ensures your Dockerfiles are processed and the images are created.

# Verify the Installation:
Go inside the controller and check if Ansible is ready:
`docker exec -it ansible_controller ansible --version`

# Project structure

ansible-masterclass/               # The root folder on your laptop
├── docker-compose.yml             # The infrastructure definition
├── Dockerfile.controller          # THIS is where Ansible is installed
├── Dockerfile.managed             # The target server blueprint
└── project/                       # Mapped into the controller container
    ├── ansible.cfg                # The Master Configuration
    ├── inventory/
    │   └── hosts.yml              # Your Docker nodes listed here
    ├── group_vars/
    │   └── all.yml                # Variables that apply to every node
    └── host_vars/
        ├── node_01.yml            # Variables specific to node_01
        └── node_02.yml            # Variables specific to node_02

# Check used ip range
`docker network ls --format "{{.Name}}" | xargs -I {} docker network inspect {} --format "{{.Name}}: {{range .IPAM.Config}}{{.Subnet}}{{end}}"`

# How to install the package from ansible galaxy:
**How to use it**: Once your container is running, you just execute `ansible-galaxy collection install -r requirements.yml` inside the controller, and it pulls down all the necessary modules for your playbooks.`

**Verify**: To verify tools are installed using `ansible-galaxy collection list` command that too inside container. 
