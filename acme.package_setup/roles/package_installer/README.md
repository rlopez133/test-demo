# Package Installer Role

Installs system packages using the appropriate package manager for the target operating system.

## Role Variables

### Required Variables

- `package_name`: (string) Name of the package to install. Example: `nginx`, `python3-pip`

### Optional Variables

- `package_state`: (string, default: `present`) Desired state of the package. Options:
  - `present`: Ensure the package is installed
  - `absent`: Ensure the package is removed
  - `latest`: Ensure the latest version is installed

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_name: nginx
        package_state: present
```

## Notes

- This role uses the `ansible.builtin.package` module which automatically detects the correct package manager (apt, yum, dnf, etc.)
- Requires elevated privileges (become/sudo) on most systems
- Idempotent: Running multiple times produces the same result
