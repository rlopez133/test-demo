# ACME Nginx Management Collection

This collection provides automation for installing, configuring, and managing the nginx web server.

## Features

- Install nginx package
- Start nginx service
- Enable nginx to start on boot
- Idempotent operations with proper state management
- Handler-based service reload/restart for configuration changes

## Requirements

- Ansible 2.15.0 or later
- Supported Linux distributions: RHEL, CentOS, Debian, Ubuntu

## Quick Start

```bash
ansible-galaxy collection install acme.nginx_management
```

Then use in a playbook:

```yaml
---
- hosts: webservers
  collections:
    - acme.nginx_management
  roles:
    - nginx
```

## Roles

### nginx

Manages nginx installation and service lifecycle.

**Variables:**

- `nginx_package_name` (default: `nginx`) - Name of the nginx package
- `nginx_package_state` (default: `present`) - Package state (present/absent)
- `nginx_service_name` (default: `nginx`) - Name of the nginx service
- `nginx_service_state` (default: `started`) - Service state (started/stopped/restarted/reloaded)
- `nginx_service_enabled` (default: `true`) - Enable service on boot

## License

GPL-3.0-or-later
