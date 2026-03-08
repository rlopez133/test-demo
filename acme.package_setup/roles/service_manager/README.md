# Service Manager Role

Manages systemd service lifecycle operations across Linux systems.

## Role Purpose

This role provides a unified interface for:
- Starting/stopping services
- Restarting/reloading services
- Enabling/disabling services at boot
- Validating service state
- Handling service readiness checks

## Supported Platforms

- Ubuntu (focal, jammy)
- Debian (9, 10, 11, 12)
- CentOS/RHEL (8, 9)
- AlmaLinux (8, 9)
- Rocky Linux (8, 9)
- Any systemd-based distribution

## Requirements

- Ansible >= 2.15.0
- systemd must be the init system
- Appropriate sudo/root privileges for service operations

## Role Variables

### Default Variables (defaults/main.yml)

```yaml
service_name: nginx                    # Service to manage
service_action: started                # Action: started, stopped, restarted, reloaded
service_enabled: true                  # Enable at boot
service_timeout: 30                    # Port wait timeout in seconds
```

### Optional Variables

```yaml
service_port: 80                       # Port to wait for (optional)
service_host: 127.0.0.1                # Host to check (optional)
```

## Usage Examples

### Start and Enable Service

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_action: started
        service_enabled: true
```

### Stop and Disable Service

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_action: stopped
        service_enabled: false
```

### Restart Service

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_action: restarted
```

### Reload Configuration

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_action: reloaded
```

### With Port Validation

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_action: started
        service_enabled: true
        service_port: 80
        service_host: "{{ ansible_default_ipv4.address }}"
```

### Selective Execution with Tags

```bash
ansible-playbook site.yml --tags service_manager
ansible-playbook site.yml --tags "service,validation"
```

## Task Flow

1. **Manage Service State**
   - Uses `ansible.builtin.systemd_service` module
   - Sets desired state (started/stopped/restarted/reloaded)
   - Configures boot behavior (enabled/disabled)
   - Reloads systemd daemon for configuration changes

2. **Wait for Service Readiness** (conditional)
   - Only runs when service is being started
   - Only runs if service state actually changed
   - Waits for specified port to be responsive
   - Timeout is configurable via `service_timeout`
   - Gracefully ignores failures (service may not expose a port)

3. **Verify Service State**
   - Queries systemd for current service state
   - Only validates when action is 'started'
   - Explicitly fails if service is not active
   - Provides detailed status information

## Handlers

This role defines two handlers for external use:

### restart service

Restarts the service with daemon reload:

```yaml
notify:
  - restart service
```

Useful when configuration files change outside this role.

### reload service

Reloads service configuration without restart:

```yaml
notify:
  - reload service
```

Useful for graceful configuration updates.

## Error Handling

- Service status validation fails explicitly if service is not active
- Port wait operations timeout gracefully without failing overall
- Uses fact queries (`changed_when: false`) for validation
- Provides clear error messages for troubleshooting

## Idempotency

All tasks are fully idempotent:
- Service state checks prevent unnecessary restarts
- Port wait only triggers on actual state changes
- Status validation uses information-only queries
- Multiple executions produce no additional changes

## Troubleshooting

### Service Not Found

```
ERROR! Service 'nonexistent' not found
```

**Solution**: Verify service name is correct and installed.

### Permission Denied

**Solution**: Ensure play is executed with appropriate privilege escalation:

```yaml
- hosts: all
  become: true
  roles:
    - acme.package_setup.service_manager
```

### Port Wait Timeout

```
WARNING: Port wait timed out - service may not expose this port
```

**Solution**: Either increase `service_timeout` or verify service actually exposes the configured port.

## Dependencies

None. Uses only Ansible builtin collections.

## Integration Example

Typical workflow combining package and service roles:

```yaml
- hosts: webservers
  become: true
  roles:
    # Step 1: Install package
    - role: acme.package_setup.package_installer
      vars:
        package_name: nginx
        package_state: present
    
    # Step 2: Start and enable service
    - role: acme.package_setup.service_manager
      vars:
        service_name: nginx
        service_action: started
        service_enabled: true
        service_port: 80
```

## License

GPL-3.0-or-later
