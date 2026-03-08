# Acme Package Setup Collection

This Ansible collection provides automation for installing system packages and managing services across Linux systems. It supports both Debian-based (Ubuntu, Debian) and RedHat-based (CentOS, RedHat) distributions.

## Features

- **Package Installation**: Install, remove, or update system packages
- **Service Management**: Start, stop, restart, or reload services
- **Multi-distribution Support**: Works with Debian, Ubuntu, CentOS, and RedHat systems
- **Idempotent Operations**: All tasks are designed to be idempotent
- **Flexible Configuration**: Override defaults via variables

## Requirements

- Ansible Core >= 2.15.0
- Target systems must have:
  - `apt` (Debian/Ubuntu) or `yum` (RedHat/CentOS)
  - `systemd` for service management
- Root or sudo access on target systems

## Installation

```bash
ansible-galaxy collection install acme.package_setup
```

## Quick Start

### Basic Usage

Create a playbook to install nginx and start the service:

```yaml
---
- name: Setup nginx
  hosts: webservers
  become: true
  roles:
    - role: acme.package_setup.package_install
      vars:
        packages_to_install:
          - nginx
        package_state: present

    - role: acme.package_setup.service_manage
      vars:
        service_name: nginx
        service_state: started
        service_enabled: true
```

### Using the Site Playbook

Run the provided site playbook:

```bash
ansible-playbook acme.package_setup.site -i inventory.ini
```

## Roles

### acme.package_setup.package_install

Installs, removes, or updates system packages.

#### Variables

- `packages_to_install` (list): List of package names to manage. Default: `['nginx']`
- `package_state` (string): State of packages - `present`, `absent`, or `latest`. Default: `present`
- `update_package_cache` (bool): Update package cache before installation (Debian). Default: `true`
- `cache_valid_time` (int): Cache validity time in seconds (Debian). Default: `3600`

#### Example

```yaml
- role: acme.package_setup.package_install
  vars:
    packages_to_install:
      - nginx
      - curl
      - git
    package_state: present
```

### acme.package_setup.service_manage

Manages system services using systemd.

#### Variables

- `service_name` (string): Name of the service to manage. Default: `nginx`
- `service_state` (string): Service state - `started`, `stopped`, `restarted`, or `reloaded`. Default: `started`
- `service_enabled` (bool): Enable service on boot. Default: `true`
- `daemon_reload` (bool): Reload systemd daemon before managing service. Default: `false`

#### Example

```yaml
- role: acme.package_setup.service_manage
  vars:
    service_name: nginx
    service_state: started
    service_enabled: true
```

## Tags

Use tags to selectively run parts of the automation:

- `package`: Run package installation tasks only
- `package_install`: Run package_install role tasks
- `service`: Run service management tasks only
- `service_manage`: Run service_manage role tasks
- `verify`: Run verification tasks
- `debug`: Display debug information

### Example

```bash
# Install packages only
ansible-playbook site.yml -i inventory.ini --tags package

# Manage services only
ansible-playbook site.yml -i inventory.ini --tags service

# Skip verification
ansible-playbook site.yml -i inventory.ini --skip-tags verify
```

## Supported Platforms

- **Debian-based**: Ubuntu 18.04+, Debian 9+
- **RedHat-based**: CentOS 7+, RedHat Enterprise Linux 7+

## Best Practices

1. **Use become**: All tasks require `become: true` to execute with root privileges
2. **Gather facts**: Facts gathering is required to detect the OS family
3. **Test first**: Always test in a non-production environment first
4. **Override defaults**: Use role variables to customize behavior for your environment

## Troubleshooting

### Service fails to start

Ensure the package is installed before managing the service. The site playbook automatically handles this ordering.

### Permission denied errors

Verify that the Ansible user has sudo access or is running as root:

```bash
ansible-playbook site.yml -i inventory.ini -u ubuntu --ask-become-pass
```

### OS detection issues

For custom or minimal distributions, verify `ansible_os_family` fact:

```bash
ansible all -i inventory.ini -m ansible.builtin.setup -a 'filter=ansible_os_family'
```

## Collection Version History

### 1.0.0

- Initial release
- Support for package installation (Debian and RedHat)
- Service management via systemd
- Multi-distribution support

## License

GPL-3.0-or-later

## Support

For issues, feature requests, or contributions, visit the [GitHub repository](https://github.com/acme/package_setup).
