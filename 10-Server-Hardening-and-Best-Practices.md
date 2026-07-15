# Chapter 10: Final System Hardening and Security Verification

## Introduction

This lab concludes the Ubuntu Server Administration Lab by verifying that all security configurations implemented throughout the project are functioning correctly. It focuses on validating the server's security posture through system updates, SSH verification, firewall inspection, service monitoring, network analysis, authentication log review, administrative privilege verification and system resource checks. By completing these verification steps, the Ubuntu server demonstrates a secure baseline suitable for remote administration and future deployment.

# 10.1 Updating the Operating System

Keeping a Linux server updated is one of the most important security practices. Software updates provide security patches, bug fixe  and performance improvements that help protect the system from known vulnerabilities.

The package repository information was refreshed using:

```bash
sudo apt update
```

Available package upgrades were then installed using:

```bash
sudo apt upgrade
```

During the update process, Ubuntu reported that two repository metadata files were "not valid yet" because of a timestamp mismatch. Despite these warnings, the remaining repositories were successfully contacted and multiple software packages were upgraded without issues.

### Evidence

_Insert Screenshot 10.1 – apt update and apt upgrade_


# 10.2 Verifying the SSH Configuration

Secure Shell (SSH) is the primary service used to remotely administer the Ubuntu server. After completing previous SSH hardening tasks, the active SSH configuration was verified using:

```bash
sudo sshd -T
```

The command displayed the effective SSH configuration currently being used by the server.

Important security settings confirmed include:

- SSH listening on TCP port 22
- Root login disabled (`PermitRootLogin no`)
- Public key authentication enabled
- Password authentication enabled
- Strict file permission checking enabled
- Modern encryption algorithms configured
- Secure MAC and cipher suites in use

### Evidence

_Insert Screenshot 10.2 – SSH effective configuration (sshd -T)_


# 10.3 Firewall Verification

The firewall configuration created in Chapter 9 was reviewed to ensure that the correct security rules remained active.

The firewall status was displayed using:

```bash
sudo ufw status verbose
```

These rules ensure that only the required network services are accessible while blocking unsolicited inbound traffic. The output confirmed:

- Firewall status: **Active**
- Default incoming policy: **Deny**
- Default outgoing policy: **Allow**
- Logging enabled (Low)
- SSH (22)
- HTTP (80)
- HTTPS (443)
- 
### Evidence

_Insert Screenshot 10.3 – UFW verbose status_

# 10.4 Reviewing Running Services

To minimise the server's attack surface, only essential services should remain active.

The currently running services were displayed using:

```bash
systemctl list-units --type=service --state=running
```

No unnecessary services were observed, indicating a minimal and well maintained server installation. The server reported 21 active services, including:

- OpenSSH Server
- Chrony (NTP)
- Cron Scheduler
- rsyslog
- Network Manager
- systemd-journald
- systemd-resolved
- PolicyKit

### Evidence

_Insert Screenshot 10.4 – Running system services_


# 10.5 Inspecting Listening Network Ports

Another important verification step is identifying which network ports are currently listening for incoming connections.

This was performed using:

```bash
sudo ss -tulnp
```

The output confirmed that only essential services were accepting network connections including:

- SSH (TCP Port 22)
- Local DNS resolver
- DHCP client
- Chrony time synchronization
No unnecessary applications were exposing additional network ports. This reduces the overall attack surface of the server.

### Evidence

_Insert Screenshot 10.5 – Listening network ports_


# 10.6 Reviewing Authentication Logs

Authentication logs provide valuable insight into both successful and failed login attempts.

To review unsuccessful authentication attempts, the following command was executed:

```bash
sudo grep "Failed" /var/log/auth.log
```

The output displayed failed SSH login attempts for an invalid user account. Monitoring these logs enables administrators to identify following

- Failed password attempts
- Invalid usernames
- Potential brute-force attacks
- Suspicious login behaviour


### Evidence

_Insert Screenshot 10.6 – Failed authentication log entries_


# 10.7 Verifying Administrative Privileges

Only trusted users should possess administrative privileges. Restricting administrative access follows the Principle of Least Privilege by ensuring that only authorized users can execute privileged commands. The members of the sudo group were verified using following command,

```bash
getent group sudo
```
The output confirmed that only the intended administrative accounts belonged to the sudo group:

- admine
- admin2

### Evidence

_Insert Screenshot 10.7 – Sudo group membership_

# 10.8 Reviewing Disk Usage

Monitoring available storage helps ensure that the operating system has sufficient space for logs, updates and normal system operation. To chcek disk usage i used following command.

```bash
df -h
```
The output showed:

- Root filesystem approximately 27% utilized
- Over 20 GB of free storage remaining
- Healthy utilization across mounted filesystems


### Evidence

_Insert Screenshot 10.8 – Disk usage_


# 10.9 Final Security Assessment

After completing all chapters of this Ubuntu Server Administration Lab, the server has been successfully configured and secured using industry standard Linux administration practices.

The completed implementation includes:

- Ubuntu Server installation
- User and group management
- Linux permissions
- Secure SSH configuration
- Service management using systemd
- Scheduled task management with cron
- Log monitoring using journalctl and system log files
- Firewall implementation using UFW
- Software package updates
- Network service verification
- Authentication monitoring
- Administrative privilege verification
- System resource monitoring

# Chapter Summary

This chapter completed the Ubuntu Server Administration Lab by verifying every major security configuration implemented throughout the project. Software packages were updated, SSH security settings were confirmed, firewall rules were validated, active services were reviewed, listening network ports were inspected, authentication logs were analyzed, administrative users were verified, and system resource utilization was assessed.

The completed server demonstrates a secure baseline for Linux system administration and provides a solid foundation for future work in cybersecurity, system administration, penetration testing and cloud infrastructure.
