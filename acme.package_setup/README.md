# ACME Package Setup Collection

This collection provides automation for installing packages and managing service states on target systems.

## Roles

### package_install
Installs and manages system packages. Supports different package managers based on the target OS.

### service_manage
Manages service state (started, stopped, restarted, etc.) and enables/disables services on boot.

## Requirements

- Ansible Core >= 2.15.0
- Target systems with supported package managers (apt, yum, dnf, etc.)

## Usage

Include the provided playbook or reference individual roles:

```yaml
---
- name: Setup packages and services
  hosts: all
  roles:
    - acme.package_setup.package_install
    - acme.package_setup.service_manage
```

## Variables

See individual role defaults/main.yml for configuration options.
