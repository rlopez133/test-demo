# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-01-01

### Added

- Initial release of ACME Package Setup collection
- `install_package` role for managing system packages across multiple package managers (apt, yum, dnf, zypper)
- `manage_service` role for managing service state and startup configuration
- Support for idempotent package installation and removal
- Support for service state management (started, stopped, restarted, reloaded)
- Comprehensive error handling with block/rescue/always patterns
- Multi-platform support (RHEL, CentOS, Ubuntu, Debian, openSUSE, SLES)
- Ansible Core >= 2.15.0 requirement
