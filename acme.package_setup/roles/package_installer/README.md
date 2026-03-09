# Package Installer Role

This role handles the installation, upgrade, and removal of system packages across different Linux distributions.

## Role Variables

### package_installer_packages
List of packages to manage. Each package must have a `name` and `state` field.

**Default:** `[]`

**Example:**
```yaml
package_installer_packages:
  - name: nginx
    state: present
  - name: old-package
    state: absent
  - name: curl
    state: latest
```

### package_installer_update_cache
Whether to update the package cache before installing packages (Debian-based systems only).

**Default:** `false`

### package_installer_cache_valid_time
Package cache validity time in seconds (Debian-based systems only).

**Default:** `3600`

## Supported Platforms

- RHEL/CentOS 8, 9 (dnf)
- Ubuntu 20.04, 22.04, 24.04 (apt)
- Debian 11, 12 (apt)

## Example Playbook

```yaml
- name: Install packages
  hosts: webservers
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_installer_update_cache: true
        package_installer_packages:
          - name: nginx
            state: present
          - name: git
            state: present
```

## License

GPL-3.0-or-later
