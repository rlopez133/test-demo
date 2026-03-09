# Package Installer Role

This role installs system packages in an idempotent manner across different Linux distributions.

## Role Variables

### Default Variables

- `package_installer_packages`: List of package names to install (default: `['nginx']`)
- `package_installer_state`: Desired state of packages - `present`, `absent`, or `latest` (default: `present`)
- `package_installer_update_cache`: Whether to update package cache before installation (default: `true`)
- `package_installer_cache_timeout`: Cache validation timeout in seconds (default: `3600`)

## Supported Platforms

- Ubuntu (Focal, Jammy)
- Debian (Bullseye, Bookworm)
- RHEL/CentOS/AlmaLinux (8, 9)

## Example Usage

```yaml
- hosts: webservers
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_installer_packages:
          - nginx
          - curl
          - git
        package_installer_state: present
```

## Task Tags

- `package_installer`: All tasks in this role
- `package`: Package-related operations
