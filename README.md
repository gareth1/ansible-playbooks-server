# Ansible Playbooks — Server automation

A small collection of Ansible playbooks to manage Ubuntu servers: patching, hardening, monitoring, backups and basic service setup. Playbooks live under the `Playbooks/` directory.

## Table of contents
- Repository layout
- Available playbooks (short list)
- Prerequisites
- Quick examples
- Inventory
- Best practices

## Repository layout

```
ansible-playbooks-server/
├── Playbooks/
│   ├── check_patches.yml
│   ├── config_backup.yml
│   ├── disk_usage_report.yml
│   ├── docker_management.yml
│   ├── firewall_setup.yml
│   ├── inventory
│   ├── inventory.template
│   ├── log_management.yml
│   ├── network_test.yml
   │   ├── ntp_config.yml
│   ├── os_version_report.yml
│   ├── patch_hosts.yml
│   ├── security_hardening.yml
│   ├── service_health.yml
│   ├── ssh_hardening.yml
│   ├── sudo_config.yml
│   ├── system_performance.yml
# Ansible Playbooks — Server automation

A small collection of Ansible playbooks to manage Ubuntu servers: patching, hardening, monitoring, backups and basic service setup. Playbooks live under the `Playbooks/` directory.

## Table of contents
- Repository layout
- Available playbooks (short list)
- Prerequisites
- Quick examples
- Inventory
- Best practices

## Repository layout

```
ansible-playbooks-server/
├── Playbooks/
│   ├── check_patches.yml
│   ├── config_backup.yml
│   ├── disk_usage_report.yml
│   ├── docker_management.yml
│   ├── firewall_setup.yml
   │   ├── inventory
│   ├── inventory.template
│   ├── log_management.yml
│   ├── network_test.yml
│   ├── ntp_config.yml
│   ├── os_version_report.yml
│   ├── patch_hosts.yml
│   ├── security_hardening.yml
│   ├── service_health.yml
│   ├── ssh_hardening.yml
│   ├── sudo_config.yml
│   ├── system_performance.yml
│   └── user_management.yml
└── README.md
```

Note: playbooks are intentionally placed together in `Playbooks/` and use the inventory file `Playbooks/inventory` (or the included `inventory.template`) as the default inventory for examples below.

## Available playbooks (short)

The repository contains the following playbooks (file names shown):

- check_patches.yml — check available package updates
- patch_hosts.yml — apply updates/patches (may reboot if required)
- disk_usage_report.yml — generate disk usage report
- os_version_report.yml — collect OS/version information
- security_hardening.yml — apply security updates and hardening
- ssh_hardening.yml — secure SSH configuration
- firewall_setup.yml — configure UFW firewall rules
- service_health.yml — basic service health checks
- system_performance.yml — collect performance metrics
- network_test.yml — network/DNS/connectivity checks
- log_management.yml — configure log rotation/cleanup
- config_backup.yml — backup important config files
- user_management.yml — create/remove/manage users and keys
- sudo_config.yml — configure sudo policies
- docker_management.yml — install/configure Docker
- ntp_config.yml — configure time synchronization

If you'd like, I can add a one-line description for each playbook in a separate commit.

## Prerequisites

- Control machine: Ansible (recommended >= 2.9). Install via pip or system package manager.
- SSH access to target hosts (key-based recommended).
- Sudo access on target hosts for playbooks that change system state.

Install Ansible quickly (example):

```bash
python3 -m pip install --user ansible
```

## Inventory

Use `Playbooks/inventory` (copy `inventory.template` to `inventory` and edit as needed). The included template has a placeholder region name (`your-aws-region`) and example private IP addresses — replace them with your real host IPs.

Example `Playbooks/inventory.template` snippet (updated):

```ini
[lanhosts]
# Replace these placeholder IPs with actual host IPs
# Example: 192.168.1.10
# Example: 192.168.1.11  # commented out for maintenance
# Example: 192.168.1.12

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

Quick connectivity test:

```bash
ansible -i Playbooks/inventory all -m ping
```

## Quick examples

Run a single playbook (default inventory path shown):

```bash
# run check patches
ansible-playbook -i Playbooks/inventory Playbooks/check_patches.yml

# apply security hardening (review inventory first)
ansible-playbook -i Playbooks/inventory Playbooks/security_hardening.yml

# generate disk usage report
ansible-playbook -i Playbooks/inventory Playbooks/disk_usage_report.yml
```

Target a group or host with -l (limit):

```bash
ansible-playbook -i Playbooks/inventory -l 192.168.1.10 Playbooks/ssh_hardening.yml
```

## Best practices

- Backup before making changes (use `config_backup.yml`).
- Test playbooks against a staging/test subset using `-l` or separate inventory groups.
- Keep secrets and private keys out of this repo — use Ansible Vault or environment-managed secrets.
- Review inventory before running any playbook that changes packages, users, or network/firewall.

## After this README change

I updated `README.md` to reflect the current repository layout (playbooks under `Playbooks/`) and to align inventory examples with `Playbooks/inventory.template` (region placeholder and sample 192.x.x.x addresses).

If you're happy with the change, review locally and commit. Example git commands you can run locally (or use GitHub Desktop):

```bash
git add README.md
git commit -m "docs: update README to match Playbooks/ layout and inventory.template changes"
```

Then push or create a PR using your usual workflow (you mentioned GitHub Desktop is ready to push).

## Questions / Next steps

- Want the one-line description for each playbook expanded? I can add them.
- Want me to also add a CONTRIBUTING.md or example inventory per environment?

---

Happy to make follow-up edits — tell me which additions you want and I'll update the README again.
