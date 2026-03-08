# ACME Package Setup Collection

This Ansible collection provides automation for package installation and service management.

## Features

- Install or remove packages using the system package manager
- Manage service state (started, stopped, enabled, disabled)
- Idempotent operations with proper state management
- Support for handlers to restart services on configuration changes

## Requirements

- Ansible Core >= 2.15.0
- Target systems: Linux (RHEL, Ubuntu, Debian, etc.)

## Included Roles

### install_package

Installs or removes packages on target systems using the native package manager.

**Variables:**
- `package_name`: Name of the package to install/remove (default: 'nginx')
- `package_state`: State of the package - present or absent (default: 'present')

### manage_service

Manages service state and enables/disables services on startup.

**Variables:**
- `service_name`: Name of the service to manage (default: 'nginx')
- `service_state`: Desired state - started, stopped, restarted, reloaded (default: 'started')
- `service_enabled`: Enable service on boot (default: true)

## Quick Start

```bash
ansible-playbook acme.package_setup.site -e "package_name=nginx package_state=present service_name=nginx service_state=started"
```

## License

GPL-3.0-or-later
