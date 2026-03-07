# Troubleshooting Guide

## Common Issues and Solutions

### 1. Package Installation Fails

#### Issue: "Package not found"
```
ERROR! collection not found: acme.package_setup
```

**Solution:**
```bash
# Install collection first
ansible-galaxy collection install acme.package_setup

# Or use requirements.yml
ansible-galaxy collection install -r collections/requirements.yml
```

#### Issue: "Package manager fails"
```
failed: [host] => {"ansible_collections": ["builtin"], "changed": false, "msg": "ERROR: command execution failed"}
```

**Solution:**
```bash
# Update package cache first
ansible all -m ansible.builtin.apt -a "update_cache=yes" -i inventory/hosts

# Check available packages
ansible all -m ansible.builtin.command -a "apt-cache search nginx" -i inventory/hosts

# Verify package name for your OS
ansible all -m ansible.builtin.setup -a "filter=ansible_distribution*" -i inventory/hosts
```

### 2. Service Management Issues

#### Issue: "Service not found"
```
failed: [host] => {"changed": false, "msg": "Service not found"}
```

**Solution:**
```bash
# Verify service is installed
ansible all -m ansible.builtin.command -a "systemctl list-units --type service" -i inventory/hosts

# Check service status manually
ansible all -m ansible.builtin.command -a "systemctl status nginx" -i inventory/hosts

# View service logs
ansible all -m ansible.builtin.command -a "journalctl -u nginx -n 50" -i inventory/hosts
```

#### Issue: "Permission denied"
```
failed: [host] => {"changed": false, "msg": "Permission denied"}
```

**Solution:**
```bash
# Ensure sudo is enabled
# In inventory/hosts:
# [all:vars]
# ansible_become=true
# ansible_become_method=sudo

# Or use command line
ansible-playbook playbooks/site.yml \
  --become \
  --become-method=sudo \
  -i inventory/hosts

# Test sudo access
ansible all -m ansible.builtin.command -a "sudo -n id" -i inventory/hosts
```

### 3. Configuration Validation Issues

#### Issue: "Configuration test failed"
```
failed: [host] => {"changed": false, "msg": "nginx -t failed"}
```

**Solution:**
```bash
# Check nginx configuration manually
ansible all -m ansible.builtin.command -a "nginx -t" -i inventory/hosts

# View nginx error log
ansible all -m ansible.builtin.command -a "tail -f /var/log/nginx/error.log" -i inventory/hosts

# Disable validation in playbook
ansible-playbook playbooks/site.yml \
  -e nginx_validate_config=false \
  -i inventory/hosts
```

### 4. Connectivity Issues

#### Issue: "Connection timeout"
```
fatal: [host]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host"}
```

**Solution:**
```bash
# Test ping connectivity
ansible all -m ansible.builtin.ping -i inventory/hosts

# Check SSH connectivity
ssh -v ansible@hostname

# Verify inventory configuration
ansible-inventory --list -i inventory/hosts

# Test with increased verbosity
ansible all -m ansible.builtin.ping -vvv -i inventory/hosts
```

#### Issue: "SSH key permission denied"
```
Permission denied (publickey)
```

**Solution:**
```bash
# Fix SSH key permissions
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
chmod 700 ~/.ssh

# Specify key in inventory
# [all:vars]
# ansible_ssh_private_key_file=~/.ssh/id_rsa

# Or command line
ansible-playbook playbooks/site.yml \
  --private-key=~/.ssh/id_rsa \
  -i inventory/hosts
```

### 5. Variable Resolution Issues

#### Issue: "Undefined variable"
```
fatal: [host]: FAILED! => {"msg": "Undefined variable 'nginx_package_name'"}
```

**Solution:**
```bash
# Check default variables
cat roles/nginx_service/defaults/main.yml

# Define variables in inventory
# [all:vars]
# nginx_package_name=nginx

# Or command line
ansible-playbook playbooks/site.yml \
  -e nginx_package_name=nginx \
  -i inventory/hosts

# View all variables for host
ansible-inventory --host hostname -i inventory/hosts
```

#### Issue: "Variable undefined in template"
```
error in variable: undefined variable
```

**Solution:**
```bash
# Debug variable values
ansible-playbook playbooks/site.yml \
  -e 'ansible_verbosity=4' \
  -i inventory/hosts

# Check role vars precedence
ansible-playbook playbooks/site.yml \
  -e 'debug_all_vars=true' \
  -i inventory/hosts
```

### 6. Playbook Syntax Issues

#### Issue: "Syntax error"
```
error: expected ':', but got 'variable'
```

**Solution:**
```bash
# Validate playbook syntax
ansible-playbook playbooks/site.yml --syntax-check

# Check YAML syntax
yaml-lint playbooks/site.yml

# Run with check mode
ansible-playbook playbooks/site.yml --check -i inventory/hosts

# View detailed parse errors
ansible-playbook playbooks/site.yml -vvvv --syntax-check
```

### 7. Idempotency Issues

#### Issue: "Task reports changed on every run"
```
changed: [host] => {...}
```

**Solution:**
```bash
# Run playbook multiple times to check idempotency
for i in {1..3}; do
  echo "Run $i:"
  ansible-playbook playbooks/site.yml -i inventory/hosts
done

# Use --check to test without making changes
ansible-playbook playbooks/site.yml --check -i inventory/hosts

# Look for hardcoded IDs or timestamps in tasks
grep -r "register" roles/nginx_service/
```

## Debug Techniques

### Enable Debug Output

```bash
# Single debug level
ansible-playbook playbooks/site.yml -v -i inventory/hosts

# Multiple debug levels (up to -vvvv)
ansible-playbook playbooks/site.yml -vvv -i inventory/hosts
```

### Add Debug Tasks

```yaml
- name: Debug variable values
  ansible.builtin.debug:
    var: nginx_package_name

- name: Debug task result
  ansible.builtin.debug:
    var: task_result
```

### Step-by-Step Execution

```bash
ansible-playbook playbooks/site.yml \
  --step \
  -i inventory/hosts
```

### Test Specific Roles

```bash
ansible-playbook -e ansible_connection=local playbooks/site.yml \
  --limit localhost \
  -i inventory/hosts
```

## Performance Issues

### Check Fact Gathering

```bash
# Disable fact gathering if not needed
ansible-playbook playbooks/site.yml \
  --gather-facts no \
  -i inventory/hosts

# Use fact caching (configured in ansible.cfg)
fact_caching = jsonfile
fact_caching_connection = /tmp/ansible_facts
fact_caching_timeout = 3600
```

### Optimize Parallel Execution

```bash
# Increase forks for parallel execution
ansible-playbook playbooks/site.yml \
  --forks 20 \
  -i inventory/hosts
```

### Profile Playbook Execution

```bash
# Use callback plugin for timing
ANSIBLE_STDOUT_CALLBACK=profile_tasks \
  ansible-playbook playbooks/site.yml -i inventory/hosts
```

## Getting Help

### Useful Commands

```bash
# List all modules
ansible-doc -l

# Get module documentation
ansible-doc ansible.builtin.package

# Check Ansible version
ansible --version

# List collection contents
ansible-galaxy collection list acme.package_setup

# Show inventory
ansible-inventory --list -i inventory/hosts
```

### Enable Logging

```bash
# Set log file (configured in ansible.cfg)
log_path = ./ansible.log

# Run playbook with logging
ansible-playbook playbooks/site.yml -i inventory/hosts

# View logs
tail -f ansible.log
grep ERROR ansible.log
```
