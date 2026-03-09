# Acme Package Setup Collection

This collection provides Ansible roles for installing packages and managing services in a consistent and idempotent manner.

## Roles

### package_installer
Installs system packages using the appropriate package manager for the target system.

**Variables:**
- `package_installer_packages`: List of package names to install (default: `[nginx]`)
- `package_installer_state`: Package state (default: `present`)

### service_manager
Manages system services including startup, stopping, reloading, and enabling services.

**Variables:**
- `service_manager_services`: List of service names to manage (default: `[nginx]`)
- `service_manager_state`: Service state (default: `started`)
- `service_manager_enabled`: Whether service should start on boot (default: `true`)

## Usage

Include the collection playbook in your automation:

```yaml
- hosts: all
  collections:
    - acme.package_setup
  tasks:
    - ansible.builtin.include_role:
        name: package_installer
    - ansible.builtin.include_role:
        name: service_manager
```

## Requirements

- Ansible 2.15 or higher
- Target systems must have a supported package manager (apt, yum, dnf, etc.)
