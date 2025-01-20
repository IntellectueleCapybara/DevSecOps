# DevSecOps

## Overview

This project automates the creation and configuration of virtual machines (VMs) using Ansible and integrates with GitLab CI for continuous integration and deployment. The project includes playbooks for setting up shared storage, creating VMs, and installing necessary packages and monitoring tools.

## Files

### `Ubuntu_server_create/TestVM_Aanmaken.yaml`

This Ansible playbook sets up shared storage on a VM. It performs the following tasks:
- Creates a mount point at `/mnt/vda`.
- Formats the storage device `/dev/vda` to `ext4`.
- Adds the storage device to `/etc/fstab`.
- Mounts all filesystems defined in `/etc/fstab`.

### `Ubuntu_server_create/Ubuntu_machine.yaml`

This Ansible playbook creates and configures VMs. It performs the following tasks:
- Prompts for the Proxmox API password.
- Updates package lists and installs Python 3 and pip.
- Installs the `proxmoxer` and `requests` Python packages.
- Installs the `community.general` Ansible collection.
- Creates VMs with specified configurations (disk size, CPU, memory, static IP).
- Adds shared storage to the VMs.
- Starts the VMs and waits for them to boot.
- Installs monitoring tools (Netdata) on the VMs.

### `Ubuntu_server_create/hosts`

This inventory file lists the hosts and their connection details for Ansible. It includes:
- `pm03`: The Proxmox server.
- `DevSecOps`: The main VM for development and security operations.
- `DevSecOpsTest`: A test VM.

### `.gitlab-ci.yml`

This GitLab CI configuration file defines the CI/CD pipeline stages and jobs. It includes:
- `setup`: Runs an Ansible playbook to set up the environment.
- `build`: Installs necessary packages and sets up Pi-hole.

## Getting Started

### Prerequisites

- Ansible
- Proxmox server
- GitLab CI