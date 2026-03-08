# ACME Package Setup Collection

This Ansible collection provides roles for managing package installation and service lifecycle, with a focus on nginx deployment.

## Overview

The `acme.package_setup` collection simplifies the deployment and configuration of nginx across multiple Linux distributions. It follows Ansible best practices for idempotence, error handling, and maintainability.

## Requirements

- **Ansible Core:** >= 2.15.0
- **Python:** 3.9 or later on control node
- **Target Hosts:** Ubuntu, Debian, CentOS, or RHEL with appropriate privileges

## Roles

### nginx_package

Installs the nginx package on target systems with proper state management.

**Variables:**
- `nginx_package_name` (default: `nginx`): Package name to install
- `nginx_package_state` (default: `present`): Package state (present or absent)
- `nginx_update_cache` (default: `true`): Update package cache before installation

**Tags:**
- `package-management`: All package-related tasks
- `nginx-install`: Nginx package installation

### nginx_service

Manages the nginx service lifecycle (start, stop, enable, disable).

**Variables:**
- `nginx_service_name` (default: `nginx`): Service name
- `nginx_service_state` (default: `started`): Service state (started, stopped, restarted, reloaded)
- `nginx_service_enabled` (default: `true`): Enable service on boot

**Tags:**
- `service-management`: All service-related tasks
- `nginx-service`: Nginx service management

## Quick Start

### Installation

Install the collection from Ansible Galaxy:

```bash
ansible-galaxy collection install acme.package_setup
```

Or from a requirements.yml file:

```yaml
collections:
  - name: acme.package_setup
    version: '>=1.0.0'
```

### Basic Usage

Run the main playbook to install and start nginx:

```bash
ansible-playbook acme.package_setup.site -i inventory.ini
```

### Custom Configuration

Override default variables in your playbook:

```yaml
- name: Custom nginx setup
  hosts: webservers
  become: true
  vars:
    nginx_package_state: present
    nginx_service_state: started
    nginx_service_enabled: true
  roles:
    - role: acme.package_setup.nginx_package
    - role: acme.package_setup.nginx_service
```

### Running Specific Tasks

Use tags to run only specific tasks:

```bash
# Install package only
ansible-playbook acme.package_setup.site -i inventory.ini -t package-management

# Manage service only
ansible-playbook acme.package_setup.site -i inventory.ini -t service-management
```

## Supported Platforms

- **Ubuntu:** 20.04, 22.04
- **Debian:** 10, 11
- **CentOS:** 8, 9
- **RHEL:** 8, 9

## License

GPL-3.0-or-later

## Author

Ansible Automation
