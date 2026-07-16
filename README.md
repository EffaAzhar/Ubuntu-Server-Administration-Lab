# Ubuntu Server Administration Lab

A hands on Ubuntu Server administration project developed to build practical Linux system administration skills within a secure virtual laboratory environment. This project documents the complete process of installing, configuring, securing and administering an Ubuntu Server. Each chapter focuses on a core administrative task commonly performed by Linux system administrators and cybersecurity professionals. The goal is not simply to execute commands but understand how each configuration contributes to building a secure server. The lab was completed on an Ubuntu Server virtual machine using a command line environment. I have documented everything using screenshots.

## Project Objectives

- Learn Ubuntu Server administration from installation to security hardening.
- Develop practical Linux command line skills.
- Understand user and group administration.
- Configure secure remote administration using OpenSSH.
- Manage Linux services with systemd.
- Monitor system activity using logs and journalctl.
- Configure and manage firewall rules using UFW.
- Apply Linux security best practices.
- Build a documented administration project suitable for cybersecurity and research portfolios.

## Environment

| Component | Details |
|-----------|---------|
| Operating System | Ubuntu Server 24.04 LTS |
| Virtualization | UTM |
| Host Machine | Apple MacBook Pro (M1) |
| Access Method | Local Console & SSH |
| Firewall | UFW (Uncomplicated Firewall) |
| Service Manager | systemd |
| Logging | rsyslog & journalctl |

# Project Structure

```
Ubuntu-Server-Administration-Lab
│
├── README.md
├── 01-installing-ubuntu-server.md
├── 02-server-network-configuration.md
├── 03-openssh-server.md
├── 04-SSH-Key-Based-Authentication.md
├── 05-SSH-Hardening.md
├── 06-User-and-Group-Administration.md
├── 07-Systemd-and-Service-Management.md
├── 08-Log-Management.md
├── 09-Firewall-Management-with-UFW.md
├── 10-Server-Hardening-and-Best-Practices.md
└── screenshots/
```

# Chapters

## Chapter 1 : Installing Ubuntu Server
- Install Ubuntu Server
- Initial system configuration
- Verify successful installation
- Basic command line navigation

## Chapter 2 : Server Network Configuration
- Configure hostname
- Verify IP configuration
- Test network connectivity
- DNS resolution
- Network verification

## Chapter 3 : OpenSSH Server
- Install OpenSSH Server
- Enable SSH service
- Verify remote connectivity
- Check SSH status

## Chapter 4 : SSH Key-Based Authentication

- Generate SSH keys
- Configure authorized keys
- Disable password dependency for authentication

## Chapter 5 : SSH Hardening
- Disable root login
- Configure SSH security options
- Validate secure remote access

## Chapter 6 : User and Group Administration
- Create users
- Modify user accounts
- Create and manage groups
- Configure sudo privileges
- Verify permissions

## Chapter 7 : Systemd and Service Management
- Understand systemd
- Manage Linux services
- Start, stop and restart services
- Enable services at boot
- Inspect service status
- Review system logs

## Chapter 8 : Log Management
- Explore Linux log files
- Monitor authentication logs
- Use journalctl
- Filter system logs
- Investigate SSH activity
- Understand log rotation

## Chapter 9 : Firewall Management with UFW
- Configure UFW
- Create firewall rules
- Allow SSH safely
- Manage HTTP and HTTPS rules
- Enable logging
- Explore application profiles

## Chapter 10 : Server Hardening and Best Practices
- Update system packages
- Verify SSH security
- Review firewall configuration
- Inspect running services
- Check listening network ports
- Review authentication logs
- Verify administrative users
- Monitor disk usage
- Perform final security assessment

# Skills Demonstrated

- Linux System Administration
- Ubuntu Server
- Bash Command Line
- OpenSSH
- SSH Key Authentication
- SSH Hardening
- User & Group Management
- File Permissions
- systemd
- Service Administration
- Linux Logging
- journalctl
- rsyslog
- Log Rotation
- UFW Firewall
- Network Security
- Server Hardening
- Linux Security Best Practices


# Learning Outcomes

By completing this project I developed practical experience in administering and securing an Ubuntu Server from the command line. Rather than following isolated tutorials the project was completed as a structured laboratory where each chapter builds upon the previous one. The result is a fully configured server with secure remote access,  service administration, logging, firewall protection and system hardening. This project also provides a strong foundation for more advanced cybersecurity topics including SIEM deployment, centralized logging, intrusion detection, threat monitoring and Linux server security.

## Author

**Effa Azhar**

GitHub: https://github.com/EffaAzhar
