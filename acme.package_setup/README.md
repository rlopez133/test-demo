# ACME Package Setup Collection

This Ansible collection provides roles for package management and service lifecycle automation.

## Included Roles

### package_installer
Installs system packages using the appropriate package manager for the target OS.

**Variables:**
- `package_name` (required): Name of the package to install
- `package_state` (default: `present`): Package state (present/absent)

### service_manager
Manages service state and enablement on the target system.

**Variables:**
- `service_name` (required): Name of the service to manage
- `service_action` (default: `started`): Service state (started/stopped/restarted/reloaded)
- `service_enabled` (default: `true`): Whether the service should be enabled at boot

## Quick Start

```bash
ansible-playbook acme.package_setup.site -e "package_name=nginx"
```

## Requirements

No external collections are required. This collection uses only Ansible built-in modules.
