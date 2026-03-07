# Contributing to ACME Package Setup Collection

Thank you for considering contributions to this collection!

## Development Setup

```bash
git clone <repository-url>
cd acme-package_setup
python -m pip install -r requirements-dev.txt
```

## Testing

Run ansible-lint to validate collection structure:

```bash
ansible-lint
```

Test playbooks with molecule:

```bash
molecule test
```

## Code Standards

- Follow Ansible naming conventions (lowercase with underscores)
- Use Fully Qualified Collection Names (FQCN) for all modules
- Include meaningful task names and descriptions
- Add tags for task categorization
- Ensure idempotency in all tasks
- Document variables in defaults/main.yml

## Pull Request Process

1. Update CHANGELOG.md with your changes
2. Ensure all tests pass
3. Submit PR with clear description of changes
4. Address any feedback from maintainers
