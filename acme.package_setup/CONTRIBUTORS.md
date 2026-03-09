# Contributors

This collection is maintained by the ACME Automation team.

## How to Contribute

We welcome contributions to this collection. Please follow these guidelines:

1. **Fork the repository** and create a feature branch
2. **Write idempotent, well-tested code** following Ansible best practices
3. **Add documentation** for any new features or roles
4. **Run linters** before submitting a pull request:
   - `ansible-lint`
   - `yamllint`
5. **Submit a pull request** with a clear description of changes

## Code Style

- Follow Ansible best practices and style guide
- Use fully qualified collection names (FQCNs) for all modules
- Include meaningful task names and descriptions
- Add tags for task categorization
- Keep roles focused and single-purpose
- Use handlers for service restarts
- Extract hardcoded values into defaults/main.yml

## License

By contributing, you agree that your contributions will be licensed under the GPL-3.0-or-later license.
