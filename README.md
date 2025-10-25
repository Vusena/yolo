# Overview
This project involved the containerization and deployment of a full-stack yolo application using Docker.


# Requirements
Install the docker engine here:
- [Docker](https://docs.docker.com/engine/install/) 

## How to launch the application 


![Alt text](image.png)

## How to run the app
Use vagrant up --provison command


Installing mongo db locally 

Downloaded the .deb file (e.g., mongodb-org-server_8.2.0_amd64.deb),
#Installing mongodb 
- cd Downlaods
- sudo dpkg -i mongodb-org-server_8.2.0_amd64.deb 
# Checking the status of mongodb 
- sudo systemctl status mongod.service
- sudo systemctl start mongod.service

#Downloading mongodb shell
-sudo dpkg -i mongodb-mongosh_2.5.8_amd64.deb 
-mongosh

#Back the application
-I ran node server.js
-Mongoose automatically connects to MongoDB at localhost:27017/yolomy.

# To fire up the client
-cd client/
-npm install 
-npm start
-if you encounter this error ---> Error: error:0308010C:digital envelope routines::unsupported
 try this command instead 
 -export NODE_OPTIONS=--openssl-legacy-provider
 -npm start





 ## IP3 - CONFIGURATION MANAGEMENT
 # Yolo App - Configuration Management Project (Stage 1)
This project demonstrates automated environment setup using **Vagrant** and **Ansible** for a containerized e-commerce application.

## Stage 1: Ansible Instrumentation

### Step 1: Environment Setup
I use **Vagrant** to provision an Ubuntu 20.04 virtual machine using Jeff Geerling’s image.  
This provides a clean, reproducible environment for deploying the e-commerce application.

### Technologies
- **Vagrant** (Virtual Machine Provisioning)
- **VirtualBox** (VM Provider)
- **Ansible** (Configuration Management)
- **Ubuntu 20.04 (geerlingguy/ubuntu2004)**

### How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/Vusena/yolo
   cd yolo-app
2. Start the virtual machine:  
   vagrant up
3. Once provisioning completes, your VM will be running with:
   Hostname: yolo-app
   Forwarded port: 3000 (access via http://localhost:3000)
   Ansible Playbook: playbook.yml (automatically triggered by Vagrant)
4. To SSH into the VM:
   vagrant ssh

 ### Step 2 Ansible Configuration Setup  
After provisioning the Vagrant VM, the next step involves configuring Ansible to automate application deployment.
Files Added:
playbook.yml – The main Ansible playbook that defines how the YOLO app environment is configured and deployed.
roles/ – Directory containing modular role definitions for each component (e.g., backend, frontend, and database).
ansible.cfg – Ansible configuration file that defines the default inventory path, disables host key checking, and ensures Ansible uses the correct Python interpreter.
hosts – The Ansible inventory file listing the target host (the Vagrant VM).

### Step 3 YOLO App Configuration Management — Stage 1 (Ansible Instrumentation)
This project automates the provisioning, configuration, and deployment of the **YOLO E-commerce App** using **Ansible** and **Vagrant**.  
It replaces manual Docker Compose orchestration with infrastructure automation through Ansible roles and playbooks.


## — Ansible Playbook Overview

The `playbook.yaml` file defines how Ansible provisions and configures the YOLO application environment.  
It uses **roles**, **variables**, **tags**, and **blocks** to ensure modular, reusable, and maintainable automation.

### Key Components

| Section | Purpose |
|----------|----------|
| `hosts: yolo` | Defines the target host group from the inventory file (`hosts`). |
| `become: yes` | Runs tasks with administrative privileges. |
| `vars` & `vars_files` | Stores variables used across roles and tasks. |
| `pre_tasks` | Updates packages before running other tasks. |
| `roles` | Modular task definitions for common setup, Docker installation, and app deployment. |
| `post_tasks` | Displays confirmation message once setup completes successfully. |

### Tags Used
| Tag | Purpose |
|------|----------|
| `setup` | For system preparation tasks |
| `docker` | For Docker-related roles |
| `backend`, `frontend`, `mongo` | For individual app components |
| `confirmation` | For post-deployment success checks |

---

## How to Run the Project
1. Start the virtual machine:
   vagrant up



 
