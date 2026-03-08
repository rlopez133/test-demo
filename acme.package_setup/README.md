# ACME Package Setup Collection

An Ansible collection for managing package installation and service lifecycle operations across Linux systems.

## Overview

This collection provides automation for:
- **Package Installation**: Install, upgrade, or remove system packages (apt/yum compatible)
- **Service Management**: Start, stop, restart, or enable systemd services

## Requirements

- Ansible Core >= 2.15.0
- Python >= 3.9 on target systems
- Supported OS families:
  - Debian/Ubuntu (focal, jammy)
  - RedHat/CentOS/EL (8, 9)

## Roles

### package_installer

Installs and manages system packages across Debian and RedHat-based systems.

**Variables** (defaults/main.yml):
- `package_name`: Name of the package to install (default: `nginx`)
- `package_state`: Desired package state - present, absent, latest (default: `present`)
- `package_update_cache`: Update package cache before install (default: `true`)
- `package_cache_timeout`: Cache validity timeout in seconds (default: `3600`)

**Example Usage**:
```yaml
- role: acme.package_setup.package_installer
  vars:
    package_name: curl
    package_state: present
```

### service_manager

Manages systemd service lifecycle operations (start, stop, restart, reload).

**Variables** (defaults/main.yml):
- `service_name`: Name of the service to manage (default: `nginx`)
- `service_action`: Desired action - started, stopped, restarted, reloaded (default: `started`)
- `service_enabled`: Enable service at boot (default: `true`)
- `service_timeout`: Timeout for port wait validation in seconds (default: `30`)
- `service_port`: Port to wait for after service start (optional, default: `80`)
- `service_host`: Host to check for port availability (optional, default: `127.0.0.1`)

**Example Usage**:
```yaml
- role: acme.package_setup.service_manager
  vars:
    service_name: nginx
    service_action: started
    service_enabled: true
```

## Playbooks

### site.yml

Main orchestration playbook that:
1. Gathers system facts
2. Installs the nginx package
3. Starts and enables the nginx service
4. Validates service status

**Usage**:
```bash
ansible-playbook acme.package_setup.playbooks.site
```

## Tags

Tasks are tagged for selective execution:

- `package` - All package installation tasks
- `package_installer` - Package installer role tasks
- `service` - All service management tasks
- `service_manager` - Service manager role tasks
- `validation` - Validation and verification tasks
- `install` - Installation tasks
- `manage` - Management tasks
- `always` - Always execute (pre/post tasks)

**Example - Run only service tasks**:
```bash
ansible-playbook site.yml --tags service
```

## Workflow

The automation implements the following workflow:

```
Step 1: Install Package
  └─ Package: nginx
  └─ State: present

Step 2: Service Management
  └─ Service: nginx
  └─ Action: started (and enabled)
```

## Task Idempotency

All tasks are designed to be idempotent:
- Package operations use state declarations (present/absent/latest)
- Service operations use systemd state management
- Validation tasks use `changed_when: false` for fact-gathering
- Only actual changes trigger handlers and notifications

## Error Handling

Each role includes:
- Pre-condition validation (OS family checks)
- Post-condition validation (package/service presence checks)
- Graceful timeout handling for service startup
- Clear error messages for troubleshooting

## Security Considerations

- No hardcoded credentials in this collection
- Service operations respect systemd security constraints
- Tasks validate before making changes (check mode compatible)
- All tasks use Fully Qualified Collection Names (FQCNs)

## License

GPL-3.0-or-later

## Author

Ansible Automation
