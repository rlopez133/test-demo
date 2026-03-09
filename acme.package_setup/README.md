# ACME Package Setup Collection

This Ansible collection provides automation for package installation and service management.

## Features

- **nginx_setup** role: Install and configure nginx web server
- Service lifecycle management (start, enable, restart)
- Full idempotency with configuration handlers
- Customizable package and service parameters

## Requirements

- Ansible 2.15.0 or later
- Target systems with package managers (apt, yum, dnf, etc.)

## Usage

### Basic Usage

```bash
ansible-playbook acme.package_setup.site -i inventory.ini
```

### Override Variables

```bash
ansible-playbook acme.package_setup.site -i inventory.ini \
  -e "nginx_package_name=nginx-full" \
  -e "nginx_service_enabled=true"
```

## Roles

### nginx_setup

Installs and configures nginx web server with optional service management.

#### Variables

- `nginx_package_name`: Package name to install (default: `nginx`)
- `nginx_package_state`: Package state (default: `present`)
- `nginx_service_name`: Service name (default: `nginx`)
- `nginx_service_state`: Service state (default: `started`)
- `nginx_service_enabled`: Enable service on boot (default: `true`)
- `nginx_service_port`: Port nginx listens on (default: `80`)
- `nginx_worker_processes`: Number of worker processes (default: `auto`)
- `nginx_worker_connections`: Max worker connections (default: `768`)

## License

GPL-3.0-or-later