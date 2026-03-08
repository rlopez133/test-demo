# Package Installer Role

Installs and manages system packages with cross-platform support for Debian and RedHat-based distributions.

## Role Variables

### Required

None - all variables have sensible defaults.

### Optional

- `package_name` (default: `nginx`): Name of the package to install/remove
- `package_state` (default: `present`): State of the package (present, absent, latest)
- `update_cache` (default: `true`): Update apt cache on Debian systems before installing
- `cache_valid_time` (default: `3600`): How long to consider apt cache valid (seconds)

## Examples

### Install a single package

```yaml
---
- name: Install Apache
  hosts: webservers
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_name: apache2
        package_state: present
```

### Install multiple packages (use with loop)

```yaml
---
- name: Install multiple packages
  hosts: all
  roles:
    - role: acme.package_setup.package_installer
  vars:
    packages:
      - curl
      - wget
      - git
  tasks:
    - name: Install packages from list
      include_role:
        name: acme.package_setup.package_installer
      vars:
        package_name: "{{ item }}"
      loop: "{{ packages }}"
```

### Remove a package

```yaml
---
- name: Remove package
  hosts: all
  roles:
    - role: acme.package_setup.package_installer
      vars:
        package_name: nginx
        package_state: absent
```

## Supported Platforms

- Red Hat Enterprise Linux 8, 9
- CentOS 8, 9
- Ubuntu 20.04, 22.04
- Debian 10, 11, 12
