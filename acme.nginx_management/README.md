# ACME Nginx Management Collection

This Ansible collection provides roles and playbooks for managing Nginx web servers, including installation, service startup, and boot-time enablement.

## Included Roles

### acme.nginx_management.install
Installs the Nginx web server package on target systems.
- Ensures the package is installed with state: present
- Fully configurable package name via defaults

### acme.nginx_management.service
Manages the Nginx service lifecycle, including starting and enabling on boot.
- Starts the Nginx service
- Enables Nginx to automatically start on system boot
- Uses handlers for idempotent service management

## Quick Start

```yaml
---
- name: Deploy and manage Nginx
  hosts: webservers
  gather_facts: true
  roles:
    - acme.nginx_management.install
    - acme.nginx_management.service
```

## Requirements

- Ansible 2.15.0 or later
- Target systems must have package management tools (apt, yum, etc.)

## Collection Dependencies

This collection uses only Ansible built-in modules and requires no external collections.

## License

GNU General Public License v3.0 or later
