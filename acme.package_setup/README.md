# ACME Package Setup Collection

A production-ready Ansible collection for managing package installation and service lifecycle on Linux systems.

## Overview

This collection provides idempotent, robust automation for:
- Installing and managing software packages
- Starting and managing systemd services
- Validating service configurations
- Cross-platform support (Debian, RHEL, Ubuntu)

## Collection Structure

```
acme.package_setup/
├── galaxy.yml
├── meta/runtime.yml
├── roles/
│   └── nginx_service/
│       ├── defaults/main.yml
│       ├── tasks/main.yml
│       └── meta/main.yml
├── playbooks/
│   └── site.yml
├── collections/
│   └── requirements.yml
└── README.md
```

## Roles

### nginx_service

Manages the complete lifecycle of nginx:
- Package installation/removal
- Service state management (started, stopped, restarted)
- Service enablement on boot
- Configuration validation
- Cross-platform compatibility

#### Variables

**defaults/main.yml:**
- `nginx_package_name`: Package name (default: `nginx`)
- `nginx_package_state`: Package state - present/absent/latest (default: `present`)
- `nginx_service_name`: Service name (default: `nginx`)
- `nginx_service_state`: Service state - started/stopped/restarted (default: `started`)
- `nginx_service_enabled`: Enable service on boot (default: `true`)
- `nginx_validate_config`: Validate configuration before starting (default: `true`)

## Playbooks

### site.yml

Main playbook that orchestrates the complete nginx setup workflow:
1. Pre-tasks: Display execution context
2. Include role: nginx_service
3. Post-tasks: Verify installation and service status

Usage:
```bash
ansible-playbook playbooks/site.yml -i inventory/hosts
```

## Requirements

- Ansible Core >= 2.15.0
- Target systems: Linux (Debian, Ubuntu, RHEL, AlmaLinux, Rocky Linux)
- Supported package managers: apt, dnf, yum, zypper
- Collections:
  - ansible.posix >= 1.1.0

## Installation

```bash
# Install from Galaxy
ansible-galaxy collection install acme.package_setup

# Or install requirements
ansible-galaxy collection install -r collections/requirements.yml
```

## Usage Examples

### Basic playbook execution
```bash
ansible-playbook playbooks/site.yml
```

### Run with specific variables
```bash
ansible-playbook playbooks/site.yml \
  -e nginx_package_state=latest \
  -e nginx_service_state=started
```

### Run only package installation
```bash
ansible-playbook playbooks/site.yml --tags package
```

### Run only service management
```bash
ansible-playbook playbooks/site.yml --tags service
```

### Validate without making changes
```bash
ansible-playbook playbooks/site.yml --check
```

## Task Tags

Tasks are tagged for selective execution:
- `package`: Package installation tasks
- `service`: Service management tasks
- `validation`: Configuration validation tasks
- `verify`: Post-execution verification
- `nginx`: All nginx-related tasks
- `always`: Tasks that run regardless of tag selection

## Error Handling

All task blocks include proper error handling:
- Tasks use `block/rescue` for graceful failure handling
- Meaningful error messages are displayed on failure
- Failed tasks prevent subsequent execution
- Check mode is supported for dry-run validation

## Idempotency

All tasks are idempotent:
- Package manager handles duplicate install requests
- Service module only acts when state differs
- Configuration validation uses check mode
- Multiple runs produce same outcome

## Supported Platforms

| OS Family | Versions | Status |
|-----------|----------|--------|
| Debian | 11, 12 | ✓ Tested |
| Ubuntu | 20.04, 22.04, 24.04 | ✓ Tested |
| RHEL | 8, 9 | ✓ Tested |
| AlmaLinux | 8, 9 | ✓ Compatible |
| Rocky Linux | 8, 9 | ✓ Compatible |

## Best Practices

1. **Always use inventory files** - Don't hardcode hosts
2. **Verify in check mode first** - Use `--check` before production runs
3. **Use vault for secrets** - Never commit credentials
4. **Review verbose output** - Use `-v` or `-vv` for troubleshooting
5. **Test in staging** - Always test in non-production environments

## Troubleshooting

### Package installation fails
- Verify package name is correct for your OS
- Update package cache: `ansible-playbook playbooks/site.yml -e nginx_package_name=nginx-latest`
- Check system package manager availability

### Service fails to start
- Run validation: `systemctl status nginx`
- Check logs: `journalctl -u nginx -n 50`
- Verify configuration: `nginx -t`

### Cross-platform issues
- Ensure target OS is supported (see Supported Platforms)
- Check ansible_os_family facts
- Review distribution-specific package names

## Contributing

Contributions are welcome! Please ensure:
- All tasks are idempotent
- Code follows Ansible best practices
- Tasks include descriptive names and tags
- Error handling is comprehensive
- Documentation is updated

## License

GPL-3.0-or-later

## Author

Ansible Automation
