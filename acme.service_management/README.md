# ACME Service Management Collection

This Ansible collection provides roles for managing services and packages on Linux systems.

## Included Roles

### nginx_deployment
Deploys and configures the Nginx web server.

**Features:**
- Installs Nginx package
- Starts Nginx service
- Enables Nginx to start on boot
- Configurable package and service names

**Usage:**
```yaml
- hosts: webservers
  roles:
    - acme.service_management.nginx_deployment
```

## Requirements

- Ansible >= 2.15.0
- Target systems must be Linux (Debian/Ubuntu/RHEL-based)

## License

GPL-3.0-or-later
