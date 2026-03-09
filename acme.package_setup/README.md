# acme.package_setup

An Ansible collection that installs the **nginx** package and ensures the
**nginx** service is running and enabled on target hosts.

## Requirements

- ansible-core >= 2.15.0
- Privilege escalation (`become`) must be available on target hosts

## Collection Structure

```
galaxy.yml
meta/runtime.yml
roles/
  nginx/
    tasks/main.yml        # Install package and manage service
    handlers/main.yml     # Restart / reload handlers
    defaults/main.yml     # Overridable default variables
    meta/main.yml         # Role metadata
playbooks/
  site.yml                # Main entry-point playbook
collections/
  requirements.yml        # External collection dependencies
```

## Roles

### `nginx`

Installs the nginx package via the system package manager and ensures the
nginx service is started and enabled at boot.

#### Default Variables

| Variable | Default | Description |
|---|---|---|
| `nginx_package_name` | `nginx` | Package name to install |
| `nginx_package_state` | `present` | Desired package state |
| `nginx_service_name` | `nginx` | System service name |
| `nginx_service_state` | `started` | Desired service runtime state |
| `nginx_service_enabled` | `true` | Enable service on boot |

## Usage

### Install the collection

```bash
ansible-galaxy collection install acme.package_setup
```

### Run the main playbook

```bash
ansible-playbook playbooks/site.yml -i inventory/hosts
```

### Run only package tasks

```bash
ansible-playbook playbooks/site.yml -i inventory/hosts --tags package
```

### Run only service tasks

```bash
ansible-playbook playbooks/site.yml -i inventory/hosts --tags service
```

### Override variables

```yaml
# group_vars/webservers.yml
nginx_package_state: latest
nginx_service_enabled: true
```

## Secret Handling

No secrets are required for this role. If future extensions require SSL
certificates or HTTP authentication, follow the vault variable convention:

```yaml
# vault_ssl_private_key: PEM-encoded private key for nginx TLS
nginx_ssl_key: "{{ vault_ssl_private_key }}"
```

## License

GPL-2.0-or-later
