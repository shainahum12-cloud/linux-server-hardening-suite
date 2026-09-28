# linux-server-hardening-suite
📫 Contact &amp; Inquiries:      Email: shainahum12@gmail.com      GitHub: shainahum12-cloud☕ Crypto Donations &amp; Support  If you find this tool useful for your infrastructure, support further open-source development:      EVM / ETH / ERC-20 / USDT / USDC:      0x943c9cb2b90ed538772f9a7f5729918777e5cd9c

# 🛡️ Linux Server Hardening & Security Suite

![Bash](https://img.shields.io/badge/Language-Bash-4EAA25.svg)
![OS](https://img.shields.io/badge/OS-Ubuntu%20%7C%20Debian%20%7C%20Kali-E95420.svg)
![License](https://img.shields.io/badge/License-Apache--2.0-blue.svg)

An automated Bash script designed to streamline system hardening, configure baseline firewall rules, secure SSH configurations, and optimize package management on Linux servers.

---

## ✨ Key Features

* **🔥 Automated UFW Setup:** Restricts inbound traffic by default while allowing essential ports (`22/SSH`, `80/HTTP`, `443/HTTPS`).
* **🔐 SSH Hardening:** Disables direct root login (`PermitRootLogin no`) and limits failed auth attempts (`MaxAuthTries 3`).
* **📦 System Updates & Cleanup:** Automates package upgrades and purges orphaned dependencies to minimize attack surface.
* **🛡️ Fail-Safe Backups:** Automatically creates timestamps for modified configuration files prior to applying changes.

---

## ⚡ Quick Start

### One-Line Installation & Execution
Run the following command as **root** or via `sudo`:

```bash
curl -sSL [https://raw.githubusercontent.com/shainahum12-cloud/linux-server-hardening-suite/main/secure-linux-server.sh](https://raw.githubusercontent.com/shainahum12-cloud/linux-server-hardening-suite/main/secure-linux-server.sh) | sudo bash


#!/usr/bin/env bash
# ==============================================================================
# Script Name: secure-linux-server.sh
# Description: Automated Linux Server Hardening & Security Audit Tool
# Author: Shai Nahum (GitHub: shainahum12-cloud)
# License: Apache-2.0
# ==============================================================================

set -euo pipefail

# Ensure script is run with root privileges
if [[ $EUID -ne 0 ]]; then
   echo "[!] This script must be run as root (use sudo)." 
   exit 1
fi

echo "=================================================="
echo "   Linux Server Hardening Suite by Shai Nahum     "
echo "=================================================="

# 1. Update System Packages
echo -e "\n[*] Updating package lists and upgrading system packages..."
apt-get update -y && apt-get upgrade -y

# 2. Configure Uncomplicated Firewall (UFW)
echo -e "\n[*] Configuring UFW Firewall..."
if command -v ufw >/dev/null 2>&1; then
    ufw default deny incoming
    ufw default allow outgoing
    ufw allow 22/tcp comment 'Allow SSH'
    ufw allow 80/tcp comment 'Allow HTTP'
    ufw allow 443/tcp comment 'Allow HTTPS'
    ufw --force enable
    echo "[+] UFW Enabled with secure defaults (SSH, HTTP, HTTPS allowed)."
else
    echo "[!] UFW is not installed. Installing UFW..."
    apt-get install -y ufw
    ufw default deny incoming
    ufw default allow outgoing
    ufw allow 22/tcp
    ufw allow 80/tcp
    ufw allow 443/tcp
    ufw --force enable
fi

# 3. Secure SSH Configuration
echo -e "\n[*] Hardening SSH Configuration..."
SSH_CONFIG="/etc/ssh/sshd_config"
if [[ -f "$SSH_CONFIG" ]]; then
    cp "$SSH_CONFIG" "${SSH_CONFIG}.bak_$(date +%F)"
    sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin no/' "$SSH_CONFIG"
    sed -i 's/^#\?MaxAuthTries.*/MaxAuthTries 3/' "$SSH_CONFIG"
    sed -i 's/^#\?X11Forwarding.*/X11Forwarding no/' "$SSH_CONFIG"
    systemctl restart sshd || systemctl restart ssh
    echo "[+] SSH hardened: Root login disabled, auth tries limited to 3."
fi

# 4. Remove Unnecessary Packages & Clean Up
echo -e "\n[*] Removing unused packages and clearing cache..."
apt-get autoremove -y && apt-get clean

echo -e "\n=================================================="
echo "   Hardening Complete! Server is now secured.    "
echo "=================================================="


