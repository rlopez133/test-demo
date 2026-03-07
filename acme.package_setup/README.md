# ACME Package Setup Collection

This Ansible collection provides roles for managing package installation and service lifecycle management.

## Roles

### nginx_package
Handles installation and configuration of the nginx package.

### nginx_service
Manages the lifecycle (start, stop, enable, disable) of the nginx service.

## Usage

Include this collection in your playbooks using the fully qualified role names:

```yaml
- name: Setup nginx
  hosts: all
  roles:
    - acme.package_setup.nginx_package
    - acme.package_setup.nginx_service
```

## Variables

All configurable variables are defined in each role's `defaults/main.yml`.

## Requirements

- Ansible 2.15.0 or later
- Target systems must have package manager (apt, yum, dnf, etc.)
