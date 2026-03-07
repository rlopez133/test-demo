# Usage Guide

## Basic Usage

### 1. Create Inventory

```ini
# inventory/hosts
[webservers]
web1.example.com ansible_user=ubuntu
web2.example.com ansible_user=ubuntu

[all:vars]
ansible_become=true
```

### 2. Run Playbook

```bash
ansible-playbook playbooks/site.yml -i inventory/hosts
```

## Advanced Usage

### Run with Variables

```bash
# Install latest nginx
ansible-playbook playbooks/site.yml \
  -e nginx_package_state=latest \
  -i inventory/hosts

# Stop nginx service
ansible-playbook playbooks/site.yml \
  -e nginx_service_state=stopped \
  -i inventory/hosts

# Disable service on boot
ansible-playbook playbooks/site.yml \
  -e nginx_service_enabled=false \
  -i inventory/hosts
```

### Use Tags for Selective Execution

```bash
# Only install packages
ansible-playbook playbooks/site.yml \
  --tags package \
  -i inventory/hosts

# Only manage services
ansible-playbook playbooks/site.yml \
  --tags service \
  -i inventory/hosts

# Skip specific tasks
ansible-playbook playbooks/site.yml \
  --skip-tags validation \
  -i inventory/hosts
```

### Dry-Run (Check Mode)

```bash
# See what would change without making changes
ansible-playbook playbooks/site.yml \
  --check \
  -i inventory/hosts

# Check mode with verbose output
ansible-playbook playbooks/site.yml \
  --check \
  -v \
  -i inventory/hosts
```

### Verbose Output

```bash
# Single verbosity level
ansible-playbook playbooks/site.yml -v -i inventory/hosts

# Multiple verbosity levels (up to -vvvv)
ansible-playbook playbooks/site.yml -vvv -i inventory/hosts

# Full debugging with task timing
ansible-playbook playbooks/site.yml \
  -vvv \
  --step \
  -i inventory/hosts
```

### Limit Execution to Specific Hosts

```bash
# Run on single host
ansible-playbook playbooks/site.yml \
  --limit web1.example.com \
  -i inventory/hosts

# Run on host group
ansible-playbook playbooks/site.yml \
  --limit webservers \
  -i inventory/hosts

# Run on multiple specific hosts
ansible-playbook playbooks/site.yml \
  --limit web1.example.com,web2.example.com \
  -i inventory/hosts
```

## Variable Customization

### Override Default Variables

**Method 1: Command line**
```bash
ansible-playbook playbooks/site.yml \
  -e nginx_package_name=nginx-latest \
  -e nginx_service_state=restarted \
  -i inventory/hosts
```

**Method 2: Group variables**
```ini
# inventory/group_vars/webservers.yml
nginx_package_name: nginx-latest
nginx_service_state: started
nginx_service_enabled: true
```

**Method 3: Host variables**
```ini
# inventory/host_vars/web1.example.com.yml
nginx_package_state: latest
nginx_validate_config: true
```

**Method 4: Playbook variables**
```yaml
---
- name: Configure nginx
  hosts: webservers
  vars:
    nginx_package_state: latest
    nginx_service_state: started
  roles:
    - nginx_service
```

## Common Scenarios

### Scenario 1: Fresh nginx Installation

```bash
ansible-playbook playbooks/site.yml \
  -e nginx_package_state=present \
  -e nginx_service_state=started \
  -e nginx_service_enabled=true \
  -i inventory/hosts
```

### Scenario 2: Update Existing Installation

```bash
ansible-playbook playbooks/site.yml \
  -e nginx_package_state=latest \
  -e nginx_service_state=restarted \
  -i inventory/hosts
```

### Scenario 3: Stop and Disable Service

```bash
ansible-playbook playbooks/site.yml \
  -e nginx_service_state=stopped \
  -e nginx_service_enabled=false \
  -i inventory/hosts
```

### Scenario 4: Remove Package

```bash
ansible-playbook playbooks/site.yml \
  -e nginx_package_state=absent \
  -i inventory/hosts
```

## Troubleshooting

### Debug Undefined Variables

```bash
ansible-playbook playbooks/site.yml \
  -e 'ansible_verbosity=4' \
  -i inventory/hosts
```

### Print All Facts

```bash
ansible all -m ansible.builtin.setup -i inventory/hosts
```

### Test Connectivity

```bash
ansible all -m ansible.builtin.ping -i inventory/hosts
```

### Validate Playbook Syntax

```bash
ansible-playbook playbooks/site.yml --syntax-check -i inventory/hosts
```

## Performance Tips

### Parallel Execution

```bash
# Run on 10 hosts in parallel (default is 5)
ansible-playbook playbooks/site.yml \
  --forks 10 \
  -i inventory/hosts
```

### Gather Facts Once

Fact caching is configured in `ansible.cfg` for improved performance.

### Skip Unnecessary Checks

```bash
ansible-playbook playbooks/site.yml \
  --gather-facts no \
  -i inventory/hosts
```

## Logging

All playbook executions are logged to `ansible.log`:

```bash
# View recent logs
tail -f ansible.log

# Search logs
grep "changed" ansible.log
grep "ERROR" ansible.log
```
