# Service Manager Role

This role manages systemd services on Linux systems, handling startup, stopping, and enablement.

## Features

- Manages services using systemd_service module
- Supports all service states (started, stopped, restarted, reloaded)
- Enables/disables services for boot startup
- Includes service status verification
- Provides detailed status feedback

## Variables

### Required
None - all variables have sensible defaults.

### Optional

- `service_name` (string, default: "nginx"): Name of the service to manage
- `service_state` (string, default: "started"): Desired state - `started`, `stopped`, `restarted`, or `reloaded`
- `service_enabled` (boolean, default: true): Whether service should start on boot

## Example Playbook

```yaml
- hosts: webservers
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_state: started
        service_enabled: true
```

## Tags

- `service` - All service-related tasks
- `service-manager` - Tasks specific to this role

## Handlers

This role defines handlers for common service operations:
- `restart service` - Restarts the service
- `reload service` - Reloads the service
- `enable service` - Enables the service

Other roles can notify these handlers to trigger service operations.

## Notes

- Requires systemd on target systems (available on modern Linux distributions)
- May require elevated privileges (sudo/root)
- Service verification queries systemd for active state when service_state is "started"
