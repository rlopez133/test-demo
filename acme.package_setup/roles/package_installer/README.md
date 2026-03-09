# Package Installer Role

This role installs and manages system packages using the native package manager of the target system.

## Purpose

The package_installer role abstracts package management across different operating systems (RedHat, Debian, etc.) by using the `ansible.builtin.package` module, which automatically selects the correct package manager.

## Variables

### Required

None. All variables have sensible defaults.

### Optional

- `package_name` (string): Name of the package to manage. Default: `nginx`
- `package_state` (string): Desired package state (`present`, `absent`). Default: `present`

## Example Usage

```yaml
- hosts: webservers
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_name: nginx
        package_state: present
```

## Tags

- `package`: All package-related tasks
- `install`: Package installation tasks
- `info`: Information gathering tasks
- `error`: Error handling tasks

## Requirements

- Ansible >= 2.15.0
- Target system with a supported package manager (apt, yum, dnf, etc.)
- Become/sudo privileges on target system

## Idempotency

This role is fully idempotent. Running it multiple times with the same variables will produce the same result without making unnecessary changes.
