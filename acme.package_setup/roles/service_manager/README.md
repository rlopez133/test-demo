# Service Manager Role

Manages service state and boot enablement on Linux systems.

## Role Variables

### Required Variables

- `service_name`: (string) Name of the service to manage. Example: `nginx`, `postgresql`

### Optional Variables

- `service_action`: (string, default: `started`) Desired state of the service. Options:
  - `started`: Ensure the service is running
  - `stopped`: Ensure the service is stopped
  - `restarted`: Restart the service
  - `reloaded`: Reload the service configuration

- `service_enabled`: (boolean, default: `true`) Whether the service should start at boot

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_action: started
        service_enabled: true
```

## Notes

- Requires elevated privileges (become/sudo)
- Service must be installed before this role can manage it
- Idempotent: Running multiple times produces the same result
- Includes verification that service is running after management actions
