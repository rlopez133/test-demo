# ACME Package Setup Collection

This collection provides roles for managing package installation and service lifecycle automation.

## Roles

### nginx_install
Installs and starts the nginx web server on target systems.

## Requirements

- Ansible 2.15.0 or later
- Target systems must have package managers configured (apt, yum, dnf, etc.)

## Usage

```bash
ansible-playbook playbooks/site.yml
```

## Variables

See individual role defaults for available variables.
