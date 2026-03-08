# Package Installer Role

Installs and manages system packages across Debian and RedHat-based Linux distributions.

## Role Purpose

This role provides a platform-agnostic interface for:
- Installing packages
- Upgrading packages to latest version
- Removing packages
- Managing package cache for optimal performance

## Supported Platforms

- Ubuntu (focal, jammy)
- Debian (9, 10, 11, 12)
- CentOS/RHEL (8, 9)
- AlmaLinux (8, 9)
- Rocky Linux (8, 9)

## Requirements

- Ansible >= 2.15.0
- Target system must have apt or yum package managers
- Appropriate sudo/root privileges for package operations

## Role Variables

### Default Variables (defaults/main.yml)

```yaml
package_name: nginx                    # Package to install
package_state: present                 # State: present, absent, latest
package_update_cache: true             # Update cache before install
package_cache_timeout: 3600            # Cache validity in seconds
```

## Usage Examples

### Basic Installation

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_name: nginx
        package_state: present
```

### Install Latest Version

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_name: curl
        package_state: latest
```

### Remove Package

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_name: apache2
        package_state: absent
```

### Selective Execution with Tags

```bash
ansible-playbook site.yml --tags package_installer
ansible-playbook site.yml --tags "package,validation"
```

## Task Flow

1. **Update Package Cache** (Debian only)
   - Updates apt cache if `package_update_cache: true`
   - Skips if cache is still valid (within `package_cache_timeout`)

2. **Install/Manage Package**
   - Detects OS family (Debian or RedHat)
   - Uses `ansible.builtin.apt` for Debian systems
   - Uses `ansible.builtin.yum` for RedHat systems
   - Applies the specified `package_state`

3. **Validate Installation**
   - Verifies package binary is in PATH
   - Only runs when `package_state: present`
   - Provides clear error messaging if validation fails

## Handlers

This role does not use handlers. Service restart operations should be handled by the service_manager role.

## Error Handling

- Tasks gracefully skip if OS family is not supported
- Package validation fails explicitly if package is not found
- Uses `ansible.builtin.command` with proper exit code validation

## Idempotency

All tasks are fully idempotent:
- Installation checks current state and skips if already present
- Cache update uses timeout to avoid unnecessary updates
- Validation uses `changed_when: false` for fact operations

## Troubleshooting

### Package Not Found

```
ERROR! Package 'nonexistent-package' not found
```

**Solution**: Verify package name is correct for the target OS distribution.

### Cache Update Fails

```
ERROR! Unable to update package cache
```

**Solution**: Ensure target system has network connectivity and appropriate repositories configured.

### Permission Denied

**Solution**: Ensure play is executed with appropriate privilege escalation (become: true)

## Dependencies

None. Uses only Ansible builtin collections.

## License

GPL-3.0-or-later
