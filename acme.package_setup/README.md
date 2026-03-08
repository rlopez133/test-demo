# ACME Package Setup Collection

A production-ready Ansible collection for managing package installation and service lifecycle.

## Overview

This collection provides automated provisioning of system packages and service management, including installation, service startup, and configuration management.

## Included Roles

### package_installer

Responsible for installing system packages and managing their lifecycle.

**Variables:**
- `package_name`: Name of the package to install (default: nginx)
- `package_state`: Desired state of the package - present/absent (default: present)
- `package_manager`: Auto-detected or explicitly set (apt, yum, dnf, zypper)

### service_manager

Responsible for managing service state and lifecycle (start, stop, restart, reload).

**Variables:**
- `service_name`: Name of the service to manage (default: nginx)
- `service_state`: Desired service state - started/stopped/restarted/reloaded (default: started)
- `service_enabled`: Whether service should auto-start on boot (default: true)

## Usage

Basic usage to install nginx and start the service:

```yaml
- name: Setup nginx
  ansible.builtin.include_role:
    name: acme.package_setup.package_installer
  vars:
    package_name: nginx
    package_state: present

- name: Start nginx service
  ansible.builtin.include_role:
    name: acme.package_setup.service_manager
  vars:
    service_name: nginx
    service_state: started
```

Or use the site.yml playbook:

```bash
ansible-playbook -i inventory acme.package_setup.site
```

## Requirements

- Ansible >= 2.15.0
- ansible.posix >= 1.1.0
- Target systems: Linux (RHEL, CentOS, Debian, Ubuntu, SUSE)

## License

GPL-3.0-or-later