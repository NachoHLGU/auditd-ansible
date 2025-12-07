# Auditd Configuration with Ansible

## Overview
This Ansible playbook automates the installation, configuration, and verification of **auditd** on an Ubuntu 24.x VM.  
Auditd is a critical Linux auditing tool that tracks system events, helping administrators monitor and secure their environment. Using Ansible ensures consistent configuration across multiple systems while minimizing manual errors.

## System Requirements
- **Operating System:** Ubuntu 24.x
- **Ansible Version:** 2.14+ (or latest stable)
- **Dependencies:** git, Python 3.x, and required Ansible modules (`ansible.builtin.apt`, `ansible.builtin.service`, `ansible.builtin.copy`, etc.)
- **VM Requirements:** At least 2 GB RAM, 1 CPU core, and 10 GB disk space recommended.

## Repository Structure
auditd-playbook.yml # Main Ansible playbook
├── roles/ # Role definitions (if used)
│ └── auditd/ # Role for installing and configuring auditd
├── files/ # Static files (audit rules, configs)
├── templates/ # Jinja2 templates for configuration
└── README.md # Project documentation

## How to Use
1. Clone the repository to your VM:
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
ansible-pull -U https://github.com/<your-username>/<your-repo>.git auditd-playbook.yml
Audit Rules

The playbook implements the following audit rules:

Monitor sudo usage: Logs all commands executed with elevated privileges.

Monitor file changes: Tracks modifications in /etc configuration files.

Monitor authentication events: Records login/logout attempts and failures.

Monitor process execution: Captures execution of critical system binaries.

Customize the rules in files/audit.rules or the relevant role directory.
GitHub Repo
     │
     ▼
ansible-pull (VM)
     │
     ▼
Auditd Installed & Configured
     │
     ▼
Event Logs Stored Locally & Monitored

Verification Steps

To confirm auditd is running and logging events:

Check auditd service status:

sudo systemctl status auditd


List active audit rules:

sudo auditctl -l


Search for specific events:

sudo ausearch -m USER_LOGIN
sudo ausearch -f /etc/passwd

Troubleshooting Tips

Auditd not starting: Check journalctl -xe and ensure no conflicting services are running.

Rules not loaded: Re-run auditctl -R /etc/audit/rules.d/audit.rules or reapply the playbook.

Permissions issues: Run ansible-pull and auditctl commands with sudo.

