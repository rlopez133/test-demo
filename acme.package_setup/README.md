# Acme Package Setup Collection

This Ansible collection provides roles for managing package installation and service lifecycle on Linux systems.

## Roles

### package_installer
Installs and manages system packages using the appropriate package manager.

**Variables:**
- `package_name`: Name of the package to install (default: nginx)
- `package_state`: Desired state of the package (default: present)

### service_manager
Manages service startup, stopping, and enabling on Linux systems.

**Variables:**
- `service_name`: Name of the service to manage (default: nginx)
- `service_state`: Desired state of the service (default: started)
- `service_enabled`: Whether service should start on boot (default: true)

## Usage

```yaml
- hosts: all
  collections:
    - acme.package_setup
  roles:
    - package_installer
    - service_manager
```

## Requirements
- Ansible 2.15.0 or later
- Target systems must be Linux-based
