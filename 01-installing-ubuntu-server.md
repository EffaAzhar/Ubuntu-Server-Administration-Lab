# Chapter 1 - Installing Ubuntu Server

## Overview

This chapter documents the deployment of Ubuntu Server 26.04 LTS within a virtualised laboratory environment using UTM on macOS. The objective was to prepare a dedicated Linux server that will be used throughout this project to practise server administration, networking, service management, logging and system hardening. Unlike a desktop operating system, Ubuntu Server provides a minimal installation focused on administration through the command line. After installation, the server was configured for secure remote administration using OpenSSH allowing all subsequent management tasks to be performed from the host operating system.

# Objectives

- Install Ubuntu Server 26.04 LTS
- Create a dedicated administrative user
- Configure the virtual machine
- Verify successful installation
- Verify network connectivity
- Install and verify OpenSSH Server
- Establish secure remote administration using SSH


# Lab Environment

| Component | Details |
|-----------|---------|
| Host System | macOS |
| Hardware | Apple MacBook Pro (Apple M1) |
| Hypervisor | UTM |
| Guest Operating System | Ubuntu Server 26.04 LTS ARM64 |
| Virtualisation Engine | QEMU |
| RAM | 4 GB |
| CPU | 2 Virtual CPUs |
| Storage | 30 GB |
| Remote Administration | OpenSSH |

# Installation Process

The Ubuntu Server ARM64 ISO was downloaded from the official Ubuntu website and installed inside a dedicated virtual machine created using UTM.

During installation:

- Ubuntu Server 26.04 LTS was installed
- Administrative user account was created
- Hostname configured as **ubuntu-server**
- Network configured automatically using DHCP
- OpenSSH Server installed
- Initial system login completed successfully

# System Verification

After installation, several commands were executed to verify that the operating system had been installed correctly.

Commands used:

```bash
whoami
hostname
pwd
uname -a
cat /etc/os-release
```

# OpenSSH Verification

The OpenSSH service was verified to ensure remote administration was available.

Command used:

```bash
sudo systemctl status ssh
```

Verification confirmed:

- SSH service installed
- SSH daemon active
- Server listening on TCP port 22
- Remote administration ready
  
# Remote Administration

Rather than continuing to manage the server directly through the virtual machine console, I configured secure remote administration using SSH. The reason of doing that the vm terminal does not allowing to scrollback therefore now this i can handle ubuntu server directly from my macOS terminal.

Connection command:

```bash
ssh admine@192.168.64.5
```

This allowed the Ubuntu Server to be administered directly from the macOS Terminal.

# Skills Demonstrated

- Ubuntu Server installation
- Virtual machine deployment
- Linux command line navigation
- System verification
- SSH service verification
- Remote Linux administration
- Basic server deployment

# Conclusion

A fully functional Ubuntu Server laboratory environment has been successfully deployed. I establish a secure remote administration using OpenSSH  providing a realistic platform for the remaining chapters of this project.
# Screenshots

## Initial Ubuntu Server Login

![Ubuntu Server Login](screenshots/01-ubuntu-server-login.png)


## System Verification

![System Verification](screenshots/02-system-verification.png)


## OpenSSH Service Running

![SSH Service](screenshots/03-ssh-service-running.png)


## Remote Administration via SSH

![SSH Remote Login](screenshots/04-remote-ssh-login.png)
