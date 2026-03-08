# ACME Package Setup Collection

This collection provides roles for managing package installation and service lifecycle on target systems.

## Roles

### acme.package_setup.nginx_install

Installs and manages the Nginx package.

#### Variables

- `nginx_package_name`: (string) Name of the Nginx package to install. Default: `nginx`
- `nginx_package_state`: (string) Desired state of the package (present/absent). Default: `present`

### acme.package_setup.nginx_service

Manages the Nginx service state (started, stopped, restarted).

#### Variables

- `nginx_service_name`: (string) Name of the Nginx service. Default: `nginx`
- `nginx_service_state`: (string) Desired service state (started/stopped/restarted/reloaded). Default: `started`
- `nginx_service_enabled`: (boolean) Enable service on boot. Default: `true`

## Playbooks

### site.yml

Main playbook that orchestrates the complete Nginx installation and service management workflow.

## Requirements

No external collection dependencies are required. All modules used are part of ansible.builtin.

## Usage

```yaml
---
- name: Deploy Nginx
  hosts: webservers
  gather_facts: true
  roles:
    - acme.package_setup.nginx_install
    - acme.package_setup.nginx_service
```

## License

GPL-3.0-or-later
