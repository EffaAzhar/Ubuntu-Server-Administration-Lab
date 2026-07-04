# Chapter 4 : Configuring Passwordless SSH Authentication

## Objective

The objective of this chapter was to improve the security and usability of remote administration by replacing password based SSH authentication with **public key authentication.** Using SSH keys provides stronger authentication than passwords while allowing secure and convenient access to the server.


## Why Use SSH Keys?

Traditional SSH authentication relies on a username and password.

Password authentication has several disadvantages such as, 

- Passwords can be guessed through brute force attacks.
- Weak passwords are vulnerable to dictionary attacks.
- Passwords may be reused across multiple systems.
- Entering passwords repeatedly becomes inconvenient during administration.

SSH key authentication solves these problems by using **asymmetric cryptography.** A key pair consists of, 

- **Private key** – stored securely on the client and never shared.
- **Public key** – copied to the server and used to verify the client's identity.

Only a client possessing the matching private key can successfully authenticate.


## Key Generation

An ED25519 SSH key pair was generated on the macOS client using:

```bash
ssh-keygen -t ed25519
```

The generated public key was then copied to the Ubuntu server and stored in:

```text
~/.ssh/authorized_keys
```

The server uses this file to determine which public keys are authorised for remote login.

## Securing the SSH Directory

Correct file permissions are required for SSH key authentication.

The following permissions were configured:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

These permissions ensure that 

| Permission | Purpose |
|------------|---------|
| `700 ~/.ssh` | Only the account owner can access the SSH directory. |
| `600 authorized_keys` | Only the owner can read or modify the authorised public keys. |

SSH refuses to use key authentication if these permissions are considered insecure.

## Authentication Process

After the public key was installed and permissions were corrected the SSH client automatically authenticated using the stored private key. The server successfully verified the corresponding public key without requiring manual password entry. This demonstrates how public key authentication simplifies secure remote administration while reducing reliance on passwords.

## Evidence

The following screenshot demonstrates the successful configuration of passwordless SSH authentication.

Sensitive information including usernames, hostnames and SSH public key material has been intentionally redacted before publication.

<p align="center">
<img src="images/chapter4-passwordless-ssh.png" width="900">
</p>


## Learning Outcomes

Through this chapter I learned:

- How SSH public key authentication works
- The difference between public and private keys
- Why ED25519 is recommended for modern SSH deployments
- How the `authorized_keys` file controls remote authentication
- Why file permissions are essential for SSH security
- How passwordless authentication improves both security and usability
- How to securely document system administration work while protecting sensitive information


## Summary

This chapter transitioned the Ubuntu server from password-based authentication to SSH key authentication. Proper file permissions were configured, authorised keys were installed successfully and secure passwordless login was verified. The result is a more secure and efficient method of administering Linux systems remotely.

