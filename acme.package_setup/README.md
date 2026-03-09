# ACME Package Setup Collection

This collection provides automated package installation and service management capabilities.

## Included Roles

### package_install
Installs and manages system packages using native package managers.

### service_manage
Manages service state (started, stopped, enabled, disabled).

## Requirements

- Ansible Core >= 2.15.0
- Target systems must have a supported package manager (apt, yum, dnf, etc.)

## Usage

Include the collection in your playbooks:

```yaml
- hosts: all
  roles:
    - acme.package_setup.package_install
    - acme.package_setup.service_manage
```

## License

GPL-3.0-or-later