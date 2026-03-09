# ACME Package Setup Collection

This collection provides roles for installing packages and managing their associated services with proper lifecycle control.

## Roles

### package_installer

Installs and manages system packages using native package managers.

**Variables:**
- `package_name`: Name of the package to install (default: nginx)
- `package_state`: Package state (present/absent) (default: present)

### service_manager

Manages service lifecycle (start, stop, enable, disable).

**Variables:**
- `service_name`: Name of the service to manage (default: nginx)
- `service_action`: Service action (started/stopped/restarted/reloaded) (default: started)
- `service_enabled`: Whether service should start on boot (default: true)

## Example Playbook

```yaml
- hosts: all
  collections:
    - acme.package_setup
  roles:
    - role: package_installer
      vars:
        package_name: nginx
        package_state: present
    - role: service_manager
      vars:
        service_name: nginx
        service_action: started
        service_enabled: true
```

## Requirements

- Ansible >= 2.15.0
- Target systems with systemd or other service managers
