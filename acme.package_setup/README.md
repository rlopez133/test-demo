# ACME Package Setup Collection

This collection provides roles for managing package installation and service lifecycle management.

## Roles

### nginx_setup
Installs the nginx package and ensures the service is started and enabled.

## Usage

```yaml
- name: Setup nginx
  ansible.builtin.include_role:
    name: acme.package_setup.nginx_setup
```

## Variables

All variables are defined in role `defaults/main.yml` and can be overridden at runtime.

- `nginx_package_name`: Name of the nginx package (default: nginx)
- `nginx_package_state`: Package state - present/absent (default: present)
- `nginx_service_name`: Name of the nginx service (default: nginx)
- `nginx_service_state`: Service state - started/stopped/restarted/reloaded (default: started)
- `nginx_service_enabled`: Whether to enable nginx on boot (default: true)
