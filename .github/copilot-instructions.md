# Ansible Lab AI Assistant Instructions

This is a local Ansible lab environment for learning and testing Ansible automation.

## Project Structure

- **`site.yml`** - Main playbook with local configuration tasks (system info, file creation, directory management)
- **`inventory.ini`** - Inventory file defining `local` host group with `localhost` using local connection
- **`env/`** - Python virtual environment with Ansible 2.19.4 and community collections installed

## Key Patterns & Conventions

### Playbook Structure
- Playbooks use the `local` host group for localhost execution
- Connection type is `local` (no SSH required)
- Tasks use Ansible built-in modules: `command`, `debug`, `file`, `copy`, `loop`
- Variables use Jinja2 templating (e.g., `{{ ansible_env.HOME }}`, `{{ ansible_date_time.date }}`)

### Common Patterns
- **Task registration**: Use `register:` to capture command output for subsequent tasks
- **Conditional execution**: `debug` module prints registered variables for verification
- **File operations**: `file` module manages directories/files with `state: directory|touch`
- **Loops**: `loop` keyword iterates over lists (files, servers, etc.)
- **Variable facts**: `ansible_env`, `ansible_date_time` provide system context

### Development Workflow
- Activate virtual environment: `source env/bin/activate` (Linux/Mac) or `env\Scripts\activate.ps1` (Windows)
- Run playbooks: `ansible-playbook -i inventory.ini site.yml`
- List inventory: `ansible-inventory -i inventory.ini --list`
- Syntax check: `ansible-playbook -i inventory.ini site.yml --syntax-check`

## Collections Available
The environment includes Ansible community collections for:
- Cloud providers (AWS, Azure, Google Cloud, DigitalOcean)
- Network vendors (Cisco, Arista, Juniper, VyOS)
- Infrastructure (Kubernetes, OpenStack, VMware, Ovirt)
- Tools (Prometheus/Grafana, SonarQube, HashiCorp)

## When Making Changes
1. Keep playbook syntax consistent with existing tasks (module names, indentation)
2. Reuse established patterns: register output → debug display → conditional logic
3. Test playbooks with `--syntax-check` before execution
4. Document complex variable references or custom paths in task `name` fields
