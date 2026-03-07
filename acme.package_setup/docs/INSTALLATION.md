# Installation Guide

## Prerequisites

- Ansible Core >= 2.15.0
- Python 3.8+
- Linux target systems (Debian, Ubuntu, RHEL, AlmaLinux, Rocky Linux)
- sudo/root access on target systems

## Installation Methods

### Method 1: From Ansible Galaxy

```bash
# Install collection from Galaxy
ansible-galaxy collection install acme.package_setup

# Verify installation
ansible-galaxy collection list | grep acme.package_setup
```

### Method 2: From Source

```bash
# Clone repository (if available)
git clone <repository-url>
cd acme-package_setup

# Build collection package
ansible-galaxy collection build

# Install from local build
ansible-galaxy collection install acme-package_setup-1.0.0.tar.gz
```

### Method 3: Using requirements.yml

```bash
# Create requirements.yml
cat > requirements.yml << EOF
collections:
  - name: acme.package_setup
    version: "1.0.0"
EOF

# Install collection and dependencies
ansible-galaxy collection install -r requirements.yml
```

## Installation Verification

```bash
# List installed collection
ansible-galaxy collection list acme.package_setup

# Verify collection structure
ls -la ~/.ansible/collections/ansible_collections/acme/package_setup/

# Test import
ansible -m ansible.builtin.debug -a "msg=test" localhost
```

## Collection Location

After installation, the collection will be located at:

```
~/.ansible/collections/ansible_collections/acme/package_setup/
```

Or in system-wide location:
```
/usr/share/ansible/collections/ansible_collections/acme/package_setup/
```

## Ansible Configuration

Ensure your `ansible.cfg` includes the collection path:

```ini
[defaults]
collections_paths = ~/.ansible/collections
```

## Next Steps

After installation:
1. Create an inventory file with your target hosts
2. Customize variables in your playbook
3. Run the playbook: `ansible-playbook playbooks/site.yml -i inventory/hosts`

See [Usage Guide](./USAGE.md) for detailed examples.
