# Acme Package Setup Collection

This Ansible collection provides roles for installing and managing system packages and services.

## Features

- **nginx_install**: Install and configure nginx package
- **nginx_service**: Manage nginx service (start, stop, enable, disable)

## Requirements

- Ansible 2.15.0 or later
- Target systems: Linux (Debian/Ubuntu, RHEL/CentOS)

## Installation

```bash
ansible-galaxy collection install acme.package_setup
```

## Usage

Include the collection roles in your playbooks:

```yaml
---
- hosts: all
  gather_facts: yes
  roles:
    - acme.package_setup.nginx_install
    - acme.package_setup.nginx_service
```

Or use the provided site.yml playbook:

```bash
ansible-playbook playbooks/site.yml
```

## Role Variables

### nginx_install

- `nginx_package_name` (default: `nginx`): Name of the nginx package to install
- `nginx_package_state` (default: `present`): Package state (present/absent/latest)

### nginx_service

- `nginx_service_name` (default: `nginx`): Name of the nginx service
- `nginx_service_state` (default: `started`): Service state (started/stopped/restarted/reloaded)
- `nginx_service_enabled` (default: `yes`): Whether to enable nginx on boot

## License

GPL-3.0-or-later
