# ACME Package Setup Collection

This Ansible collection provides automation for installing packages and managing their associated services.

## Overview

The `acme.package_setup` collection streamlines the installation and lifecycle management of system packages, specifically nginx in this implementation. It follows Ansible best practices for idempotency, error handling, and multi-platform support.

## Requirements

- Ansible Core >= 2.15.0
- Python >= 3.9
- Supported OS families: RedHat (CentOS, RHEL, Rocky, Alma), Debian (Debian, Ubuntu)

## Included Roles

### nginx_install

Installs the nginx package on target systems.

**Variables:**
- `package_name` (default: `nginx`) - Name of the package to install
- `package_state` (default: `present`) - Package state (present/absent/latest)
- `package_version` (default: `""`) - Specific version to install (optional)

**Example:**
```yaml
- hosts: webservers
  roles:
    - role: acme.package_setup.nginx_install
      vars:
        package_name: nginx
        package_state: present
```

### nginx_service

Manages the nginx service state and startup behavior.

**Variables:**
- `service_name` (default: `nginx`) - Name of the service to manage
- `service_state` (default: `started`) - Service state (started/stopped/restarted/reloaded)
- `service_enabled` (default: `yes`) - Enable service on boot
- `service_daemon_reload` (default: `false`) - Reload systemd daemon

**Handlers:**
- `Restart nginx service` - Restart the nginx service
- `Reload nginx service` - Reload the nginx service configuration

**Example:**
```yaml
- hosts: webservers
  roles:
    - role: acme.package_setup.nginx_service
      vars:
        service_name: nginx
        service_state: started
        service_enabled: yes
```

## Usage

### Basic Example

Run the complete playbook to install and start nginx:

```bash
ansible-playbook acme.package_setup.playbooks.site
```

### Install Only

```bash
ansible-playbook acme.package_setup.playbooks.site --tags install
```

### Service Management Only

```bash
ansible-playbook acme.package_setup.playbooks.site --tags service
```

### Custom Variables

```bash
ansible-playbook acme.package_setup.playbooks.site \
  -e package_state=latest \
  -e service_state=started
```

## Tags

- `install` - Package installation tasks
- `service` - Service management tasks
- `package` - Package-related operations
- `nginx` - nginx-specific tasks
- `nginx_install` - nginx installation tasks
- `nginx_service` - nginx service tasks
- `systemd` - systemd-related tasks

## Platform Support

- **Red Hat Enterprise Linux** 8, 9
- **CentOS/Rocky/Alma Linux** 8, 9
- **Ubuntu** 20.04, 22.04 LTS
- **Debian** 11, 12

## License

GPL-3.0-or-later

## Support

For issues, questions, or contributions, please refer to the project repository.
