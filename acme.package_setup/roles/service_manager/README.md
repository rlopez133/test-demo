# Service Manager Role

Manages system service states (start, stop, restart, reload) and configures service startup behavior using systemd.

## Role Variables

### Required

None - all variables have sensible defaults.

### Optional

- `service_name` (default: `nginx`): Name of the service to manage
- `service_state` (default: `started`): State of the service (started, stopped, restarted, reloaded)
- `service_enabled` (default: `true`): Whether to enable the service on boot
- `daemon_reload` (default: `false`): Perform systemd daemon reload before managing service

## Examples

### Start and enable a service

```yaml
---
- name: Start nginx
  hosts: webservers
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_state: started
        service_enabled: true
```

### Stop a service

```yaml
---
- name: Stop apache2
  hosts: webservers
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: apache2
        service_state: stopped
        service_enabled: false
```

### Restart a service

```yaml
---
- name: Restart nginx
  hosts: webservers
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_state: restarted
```

### Reload service configuration

```yaml
---
- name: Reload nginx config
  hosts: webservers
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_state: reloaded
```

## Supported Platforms

- Red Hat Enterprise Linux 8, 9
- CentOS 8, 9
- Ubuntu 20.04, 22.04
- Debian 10, 11, 12

## Notes

This role uses `ansible.builtin.systemd_service` module and requires systems with systemd.
