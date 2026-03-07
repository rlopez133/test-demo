# Changelog

All notable changes to this project will be documented in this file.

## [1.0.0] - 2024-01-01

### Added
- Initial release of acme.package_setup collection
- `nginx_install` role for package installation on RHEL and Debian-based systems
- `nginx_service` role for service lifecycle management
- Support for RHEL 8/9, Ubuntu 20.04/22.04, and Debian 11/12
- Comprehensive playbook (site.yml) for complete nginx setup
- Handler-based service restart/reload pattern
- Multi-platform compatibility with yum and apt modules
