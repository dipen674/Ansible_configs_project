# Ansible Deployment Configuration

This repository contains Ansible configuration for automating the deployment of applications to remote machines. The playbook pulls Docker images from container registries and deploys them on target servers.

## Related Repository

This Ansible deployment is executed from the Jenkins pipeline defined in:
**[Simple_Java_TM Repository](https://github.com/dipen674/Simple_Java_TM.git)**

- **`docker` branch** - Contains Jenkins pipeline code using DockerHub
- **`harbor` branch** - Contains Jenkins pipeline code using Harbor registry

## Branch Information

This repository has different branches for different container registry implementations:

- **`docker`** - Pulls Docker images from **DockerHub** registry
- **`main`** - Pulls Docker images from **Harbor** registry

### Cloning the Repository

Choose the appropriate branch based on your container registry:

```bash
# For DockerHub registry
git clone -b docker <repository-url>

# For Harbor registry
git clone -b main <repository-url>

```

## Project Structure

```
.
├── ansible.cfg          # Ansible configuration file (defines default settings)
├── inventory.ini        # Inventory file listing target hosts and groups
├── playbook.yaml        # Main playbook that orchestrates the deployment
└── roles
    └── deploy           # Deployment role containing all automation logic
        ├── tasks        # Task files that define deployment steps
        │   ├── 01_setup.yaml      # Initial setup and prerequisites
        │   ├── 02_configs.yaml    # Configuration management
        │   ├── 03_deploy.yaml     # Application deployment tasks
        │   ├── 04_cleanup.yaml    # Post-deployment cleanup
        │   └── main.yaml          # Main task file that includes all tasks
        ├── templates    # Jinja2 templates for configuration files
        └── vars         # Variables used throughout the deployment
            └── main.yaml
```

## File Descriptions

### Core Files

- **`ansible.cfg`** - Defines Ansible behavior such as inventory location, SSH settings, privilege escalation, and other runtime configurations

- **`inventory.ini`** - Contains the list of target servers

- **`playbook.yaml`** - The main entry point that defines which roles to run
### Role Structure (`roles/deploy/`)

The deployment logic is organized into a role for better modularity and reusability:

#### Tasks (`tasks/`)
- **`01_setup.yaml`** - Handles initial system setup. Here we have created directory
- **`02_configs.yaml`** - Manages application and system configuration files
- **`03_deploy.yaml`** - Performs the actual application deployment steps
- **`04_cleanup.yaml`** - Cleans up dangling images
- **`main.yaml`** - Includes all task files in the correct order

#### Templates (`templates/`)
- Contains Jinja2 template to store environment variables

#### Variables (`vars/`)
- **`main.yaml`** - Defines role-specific variables used throughout the deployment tasks

## Usage

### Prerequisites
- Ansible installed on the control machine
- SSH access to target hosts
- Appropriate permissions on remote machines


```

## Configuration

1. Update `inventory.ini` with your target hosts
2. Modify variables in `roles/deploy/vars/main.yaml` as needed
3. Adjust `ansible.cfg` for your environment
4. Run the playbook to deploy your application
