# Service Manager Role

This role manages the state and enablement of system services using systemd.

## Role Variables

### service_manager_services
List of services to manage. Each service must have a `name` and `state` field.

**Default:** `[]`

**Example:**
```yaml
service_manager_services:
  - name: nginx
    state: started
    enabled: true
  - name: apache2
    state: stopped
    enabled: false
```

### service_manager_enabled
Default enablement state for services on boot.

**Default:** `true`

### service_manager_daemon_reload
Whether to reload systemd daemon before managing services.

**Default:** `false`

## Service States

- `started`: Ensure service is running
- `stopped`: Ensure service is stopped
- `restarted`: Restart the service
- `reloaded`: Reload the service configuration

## Supported Platforms

- RHEL/CentOS 8, 9
- Ubuntu 20.04, 22.04, 24.04
- Debian 11, 12

Requires systemd as the init system.

## Example Playbook

```yaml
- name: Manage services
  hosts: webservers
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_manager_services:
          - name: nginx
            state: started
            enabled: true
          - name: ssh
            state: started
            enabled: true
```

## License

GPL-3.0-or-later
