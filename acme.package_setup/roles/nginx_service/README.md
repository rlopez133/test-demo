# Ansible Role: nginx_service

Manages the nginx service lifecycle, including start, stop, restart, and boot-time enablement.

## Requirements

- Ansible >= 2.15.0
- Root or sudo access
- nginx package installed (use `acme.package_setup.nginx_install` role)
- systemd init system

## Role Variables

### Default Variables

```yaml
service_name: nginx                    # Service name to manage
service_state: started                 # Service state: started|stopped|restarted|reloaded
service_enabled: yes                   # Enable on boot: yes|no
service_daemon_reload: false           # Reload systemd daemon: true|false
```

## Dependencies

- nginx package must be installed

## Handlers

- `Restart nginx service` - Restarts the nginx service
- `Reload nginx service` - Reloads nginx configuration without full restart

## Example Playbook

```yaml
---
- hosts: webservers
  become: yes
  roles:
    - role: acme.package_setup.nginx_service
      vars:
        service_name: nginx
        service_state: started
        service_enabled: yes
```

## Notes

- Service state is verified after management with appropriate failure conditions
- Handlers allow configuration changes to trigger service reload/restart
- systemd module is used for reliable service management
- Service status verification confirms ActiveState is 'active' when service_state is 'started'

## License

GPL-3.0-or-later
