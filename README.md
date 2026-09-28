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
