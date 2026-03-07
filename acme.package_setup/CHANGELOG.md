# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-01-01

### Added
- Initial release of acme.package_setup collection
- nginx_service role for package and service management
- Site playbook with pre and post-task verification
- Support for Debian, Ubuntu, and RHEL-based systems
- Configuration validation before service startup
- Comprehensive error handling with block/rescue
- Task tagging for selective execution
- Full idempotency for all tasks
- Extensive documentation and examples

### Features
- Package installation with state management
- Service lifecycle management (start, stop, restart)
- Service enablement on boot
- Cross-platform compatibility
- Configuration validation
- Detailed logging and verification
