# ansible_xray

# Ansible Playbook for Automated Deployment, Configuration, and Autostart of XRAY Service with Dual Configuration

## Overview

This Ansible playbook provides **automated deployment**, **configuration**, and **autostart** capabilities for the XRAY service with support for **two configurations**:

- **Shadowsocks** - Lightweight SOCKS5 proxy for secure communications
- **VLESS Reality** - Next-generation protocol with enhanced security features

## Features

- **Automated Deployment**: Installs all necessary dependencies and XRAY binaries
- **Dual Configuration**: Configures both Shadowsocks and VLESS Reality protocols
- **Service Management**: Sets up automatic startup on system boot
- **Easy Maintenance**: Simple install and update procedures

## Prerequisites

- Control machine with Python 3.12 
- Target servers with:
  - Modern Ubuntu or Debian OS installed
  - SSH access with sudo privileges
  - Minimum 1GB RAM, 10GB disk space

## Install

1. Clone Git Repository:
`git clone https://github.com/dex2code/ansible_xray.git && cd ansible_xray`

2. Install Python VENV:
`python3 -m venv ./.venv`

3. Activate Python VENV:
`source ./.venv/bin/activate`

4. Install requirements:
`pip install -r ./requirements.txt`

5. Edit `inventory.yaml` to set up correct settings

6. Run installation playbook:
`./.venv/bin/ansible-playbook -i ./inventory.yaml ./playbook_install.yaml`

7. Import configurations into your mobile app using the QR codes in created PNG directory

8. Deactivate Python VENV:
`deactivate`

## Update xray binaries to current version:

`./.venv/bin/ansible-playbook -i ./inventory.yaml ./playbook_update.yaml`

## Uninstall xray binaries and remove service:

`./.venv/bin/ansible-playbook -i ./inventory.yaml ./playbook_uninstall.yaml`

## Service management

After deployment, manage the service on remote host with:

Check service status: `sudo systemctl status xray`

View logs: `sudo journalctl -u xray -f`

Restart service: `sudo systemctl restart xray`

Stop service: `sudo systemctl stop xray`

Disable autostart: `sudo systemctl disable xray`

## Monitoring and Logs

Binary Location: `/opt/xray`

Log Location: `/opt/xray/access.log` and `/opt/xray/error.log`

Configuration: `/opt/xray/config.json`

## Troubleshooting

Common issues and solutions:

- Port Conflicts: Check if ports from `inventory.yaml` are in use

- Permission Issues: Ensure proper user/group permissions

- Firewall Blocking: Verify firewall rules allow traffic

- Service Not Starting: Check logs with journalctl -u xray