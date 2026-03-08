# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-01-01

### Added

- Initial release of acme.package_setup collection
- `package_install` role for installing system packages
  - Support for Debian-based systems (apt)
  - Support for RedHat-based systems (yum)
  - Configurable package lists and states
  - Package cache management
- `service_manage` role for managing systemd services
  - Start, stop, restart, and reload services
  - Enable/disable services on boot
  - Daemon reload support
- Main playbook (`site.yml`) orchestrating both roles
- Comprehensive documentation and examples
- Multi-distribution support (Debian, Ubuntu, CentOS, RedHat)
- Tag-based task selection
