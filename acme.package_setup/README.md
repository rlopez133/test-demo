# ACME Package Setup Collection

This collection provides automation for managing system packages and services.

## Features

- Install and manage system packages
- Start and manage service states

## Requirements

- Ansible >= 2.15.0
- ansible.posix collection >= 1.1.0

## Installation

```bash
ansible-galaxy collection install acme.package_setup
```

## Included Roles

### package_installer
Installs and manages system packages with support for multiple package managers.

### service_manager
Manages system service states (started, stopped, enabled, disabled).

## Usage

```yaml
---
- name: Setup packages and services
  hosts: all
  collections:
    - acme.package_setup
  roles:
    - package_installer
    - service_manager
```

## Variable Documentation

See individual role directories for variable documentation and examples.
