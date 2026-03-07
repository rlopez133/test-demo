# ACME Package Setup Collection

This Ansible collection provides roles for managing package installation and service lifecycle on target systems.

## Features

- Install and manage system packages
- Start and enable services
- Idempotent operations
- Configurable package names and service names

## Included Roles

### install_packages

Installs system packages using platform-specific package managers.

**Variables:**
- `install_packages_list`: List of packages to install (default: [nginx])
- `install_packages_state`: Package state (default: present)

### manage_services

Manages service lifecycle (start, stop, enable, disable).

**Variables:**
- `manage_services_list`: List of services to manage
- `manage_services_action`: Service state (default: started)
- `manage_services_enabled`: Enable service on boot (default: true)

## Usage

```yaml
---
- hosts: all
  collections:
    - acme.package_setup
  roles:
    - role: install_packages
      vars:
        install_packages_list:
          - nginx
          - curl
    - role: manage_services
      vars:
        manage_services_list:
          - nginx
        manage_services_action: started
```

## Requirements

- Ansible >= 2.15.0
- Target systems must have sudo access for package and service management

## License

GPL-3.0-or-later
