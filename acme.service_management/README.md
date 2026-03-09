# ACME Service Management Collection

A collection for managing services on Linux systems, including installation, startup, and boot configuration.

## Features

- Install and manage service packages (e.g., nginx, apache2)
- Start and stop services
- Enable/disable services on system boot
- Idempotent operations ensuring repeatable automation

## Roles

### service_installer

Installs packages required for services.

**Variables:**
- `service_package_name`: Name of the package to install (default: nginx)
- `service_package_state`: Package state - present or absent (default: present)

### service_controller

Manages service state and boot configuration.

**Variables:**
- `service_name`: Name of the service to manage (default: nginx)
- `service_state`: Desired service state - started or stopped (default: started)
- `service_enabled`: Whether service should auto-start on boot (default: true)

## Usage

Include the collection playbook in your automation:

```yaml
- name: Manage services
  hosts: all
  collections:
    - acme.service_management
  roles:
    - service_installer
    - service_controller
```

Override defaults as needed:

```yaml
- name: Install and manage Apache
  hosts: webservers
  collections:
    - acme.service_management
  roles:
    - role: service_installer
      vars:
        service_package_name: apache2
    - role: service_controller
      vars:
        service_name: apache2
```

## Requirements

- Ansible 2.15.0 or higher
- Target systems: Linux (Debian/RHEL-based distributions)

## License

GPL-3.0-or-later
