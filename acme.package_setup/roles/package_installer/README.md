# Package Installer Role

This role installs and manages system packages using the native package manager for the target system.

## Features

- Detects OS family (Debian/Ubuntu vs RHEL/CentOS)
- Uses apt for Debian-based systems
- Uses yum for RedHat-based systems
- Supports package installation, removal, and latest version updates
- Optionally updates package cache before installation
- Provides installation status feedback

## Variables

### Required
None - all variables have sensible defaults.

### Optional

- `package_name` (string, default: "nginx"): Name of the package to manage
- `package_state` (string, default: "present"): Desired state - `present`, `absent`, or `latest`
- `update_package_cache` (boolean, default: false): Whether to update package cache before installation

## Example Playbook

```yaml
- hosts: webservers
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_name: nginx
        package_state: present
        update_package_cache: true
```

## Tags

- `package` - All package-related tasks
- `package-installer` - Tasks specific to this role

## Notes

- Requires Python on target systems (Ansible standard requirement)
- Requires package manager (apt or yum) on target systems
- May require elevated privileges (sudo/root)
