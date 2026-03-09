# Service Manager Role

This role manages system services in an idempotent manner using systemd.

## Role Variables

### Default Variables

- `service_manager_services`: List of service names to manage (default: `['nginx']`)
- `service_manager_state`: Desired state - `started`, `stopped`, `restarted`, or `reloaded` (default: `started`)
- `service_manager_enabled`: Whether service should start on boot (default: `true`)
- `service_manager_daemon_reload`: Whether to reload systemd daemon before managing services (default: `false`)

## Supported Platforms

- Ubuntu (Focal, Jammy)
- Debian (Bullseye, Bookworm)
- RHEL/CentOS/AlmaLinux (8, 9)

## Example Usage

```yaml
- hosts: webservers
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_manager_services:
          - nginx
          - postgresql
        service_manager_state: started
        service_manager_enabled: true
```

## Task Tags

- `service_manager`: All tasks in this role
- `service`: Service-related operations

## Handlers

- `restart services`: Restarts all managed services
