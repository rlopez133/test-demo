# Ansible Role: nginx_install

Installs the nginx web server package on target systems supporting both RHEL and Debian-based distributions.

## Requirements

- Ansible >= 2.15.0
- Root or sudo access
- Supported OS: RHEL 8/9, CentOS, Ubuntu 20.04+, Debian 11+

## Role Variables

### Default Variables

```yaml
package_name: nginx                    # Name of package to install
package_state: present                 # Package state: present|absent|latest
package_version: ""                    # Optional specific version
```

## Dependencies

None

## Example Playbook

```yaml
---
- hosts: webservers
  become: yes
  roles:
    - role: acme.package_setup.nginx_install
      vars:
        package_name: nginx
        package_state: present
```

## Notes

- This role uses package manager detection (yum for RedHat, apt for Debian)
- The `update_cache` option is enabled on Debian systems
- Install results are registered for downstream tasks
- All tasks are tagged with `package`, `nginx`, and `nginx_install` for selective execution

## License

GPL-3.0-or-later
