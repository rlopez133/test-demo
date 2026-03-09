# ACME Package Setup Collection

This Ansible collection provides roles for managing package installation and service lifecycle management.

## Roles

### package_installer
Installs and manages system packages using the appropriate package manager for the target system.

### service_manager
Manages service state (started, stopped, enabled, disabled) for system services.

## Requirements

- Ansible Core >= 2.15.0
- Target systems must have appropriate package managers installed (apt, dnf, etc.)

## Usage

Include this collection in your playbooks:

```yaml
- name: Setup packages and services
  hosts: all
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_installer_packages:
          - name: nginx
            state: present
    - role: acme.package_setup.service_manager
      vars:
        service_manager_services:
          - name: nginx
            state: started
            enabled: true
```

## License

GPL-3.0-or-later
