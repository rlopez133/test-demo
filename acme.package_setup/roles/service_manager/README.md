# Service Manager Role

This role manages the lifecycle of system services using systemd, including starting, stopping, enabling, and disabling services.

## Purpose

The service_manager role provides a standardized way to manage services across systems. It handles service state transitions (start, stop, restart, reload) and boot-time enablement.

## Variables

### Required

None. All variables have sensible defaults.

### Optional

- `service_name` (string): Name of the service to manage. Default: `nginx`
- `service_action` (string): Desired service action (`started`, `stopped`, `restarted`, `reloaded`). Default: `started`
- `service_enabled` (boolean): Whether service should auto-start on boot. Default: `true`

## Example Usage

```yaml
- hosts: webservers
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_action: started
        service_enabled: true
```

## Tags

- `service`: All service-related tasks
- `manage`: Service management tasks
- `verify`: Service verification tasks
- `info`: Information gathering and display tasks
- `error`: Error handling tasks

## Requirements

- Ansible >= 2.15.0
- systemd service manager on target system
- Become/sudo privileges on target system

## Idempotency

This role is fully idempotent. It checks current service state before making changes and only takes action when necessary.

## Handlers

This role includes handlers for:
- Service restart (triggered by `restart <service_name>`)
- Service reload (triggered by `reload <service_name>`)
- Service enable on boot (triggered by `enable <service_name>`)
