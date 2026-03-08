# ACME Package Setup Collection

This Ansible collection provides roles for managing package installation and service lifecycle on target systems.

## Requirements

- Ansible Core >= 2.15.0
- Target systems with support for package managers (apt, yum, dnf, etc.)

## Roles

### package_manager
Installs or removes packages on target systems using the appropriate package manager for the OS family.

**Default Variables:**
- `package_name`: Name of the package to manage (default: 'nginx')
- `package_state`: Package state - present or absent (default: 'present')

### service_controller
Manages service state (started, stopped, restarted, reloaded) and enables/disables services at boot.

**Default Variables:**
- `service_name`: Name of the service to manage (default: 'nginx')
- `service_state`: Service state - started, stopped, restarted, reloaded (default: 'started')
- `service_enabled`: Enable service at boot (default: true)

## Usage

```yaml
---
- hosts: webservers
  collections:
    - acme.package_setup
  vars:
    package_name: nginx
    package_state: present
    service_name: nginx
    service_state: started
    service_enabled: true
  roles:
    - package_manager
    - service_controller
```

## License

GPL-3.0-or-later
