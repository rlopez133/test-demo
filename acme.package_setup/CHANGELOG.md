# Changelog

All notable changes to this collection will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-01-01

### Added

- Initial release of acme.package_setup collection
- nginx_setup role for installing and managing nginx web server
- Support for multiple Linux distributions (Ubuntu, Debian, EL, AlmaLinux, Rocky)
- Idempotent package installation and service management
- Configuration validation tasks
- Customizable variables for package names, service states, and nginx tuning parameters
- Handler-based service restart and reload
