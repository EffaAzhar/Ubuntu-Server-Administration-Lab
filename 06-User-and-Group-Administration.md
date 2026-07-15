# Chapter 6: User and Group Administration

## Objective

This chapter demonstrates how to manage users and groups on an Ubuntu Server. The lab covers creating user accounts, assigning administrative privileges, creating custom groups, configuring directory permissions and verifying user access. These are fundamental tasks performed by Linux system administrators to implement **role based access control (RBAC)** and maintain secure multi user environments.

# Why User and Group Management Matters

Linux is a multi user operating system where access to files, directories and system resources is controlled through users and groups. Proper user administration helps to achieve following,
- Separate administrator and standard user accounts
- Apply Principle of Least Privilege
- Organize users based on organizational roles
- Protect sensitive resources from unauthorized access
- Simplify permission management for shared directories
## Step 1: Verify the Current User

Before making administrative changes I confirmed the identity of the logged in user.

```bash
whoami
```

## Step 2: Display User Information

The `id` command displays the current user's identity, primary group and supplementary group memberships.

```bash
id
```
output:

```text
uid=1000(admine)
gid=1000(admine)
groups=1000(admine),27(sudo),...
```

## Step 3: View Existing User Accounts

Linux stores local user information inside the `/etc/passwd` file.

```bash
cat /etc/passwd
```

To display only regular user accounts (UID ≥ 1000):

```bash
awk -F: '$3 >= 1000 {print $1}' /etc/passwd
```

## Step 4: Create a User with useradd

A new user account was created using the `useradd` command.

```bash
sudo useradd admin2
```

The account was verified using:

```bash
id admin2
```

output:

```text
uid=1001(admin2)
gid=1001(admin2)
```
Unlike `adduser` the `useradd` command creates a basic account with minimal configuration, making it suitable for scripting and automated administration tasks.

## Step 5: Grant Administrative Privileges

Administrative permissions were granted by adding the user to the `sudo` group.

```bash
sudo usermod -aG sudo admin2
```
contains two important options:

| Option | Description |
|----------|-------------|
| `-G` | Specifies one or more supplementary groups |
| `-a` | Appends the new group while preserving existing group memberships |

The `-a` (append) option is essential because omitting it would replace all existing supplementary groups with the specified group.
Verify the group membership:

```bash
groups admin2
```

Example output:

```text
admin2 : admin2 sudo
```
# Primary vs Supplementary Groups

Each Linux user has one **primary group** and may belong to multiple **supplementary groups**.

### Primary Group

- Assigned when the user is created
- Usually has the same name as the user
- Newly created files inherit this group by default

Example:

```text
User:
admin2

Primary Group:
admin2
```
### Supplementary Groups

Supplementary groups provide additional permissions without changing the primary group.

Examples include:

- sudo
- developers
- docker
- www-data

For example:

```text
admin2 : admin2 sudo
```
Here:

- `admin2` is the primary group.
- `sudo` is a supplementary group that grants administrative privileges.

## Lab Evidence: User Creation and Administrative Group Assignment

The following screenshot demonstrates:

- Identifying the current user
- Viewing user information
- Listing local accounts
- Creating a new user
- Assigning administrative privileges using the `sudo` group

![User Management](screenshots/06-01-user-management.png)


## Step 6: Create a User with adduser

Ubuntu also provides the higher level `adduser` utility.

```bash
sudo adduser prince
```

Unlike `useradd`, `adduser`:

- Creates the user's home directory automatically
- Prompts for a password
- Allows optional user information
- Applies Ubuntu's recommended defaults

The new account was verified using:

```bash
id prince
```

## Step 7: Create a Custom Group

A custom group named `developers` was created.

```bash
sudo groupadd developers
```

Verify:

```bash
grep developers /etc/group
```

Example output:

```text
developers:x:1003:
```
## Step 8: Add a User to the Developers Group

The user `prince` was added to the `developers` supplementary group.

```bash
sudo usermod -aG developers prince
```

Verify:

```bash
groups prince
```

Example output:

```text
prince : prince users developers
```

This confirms that the account now belongs to multiple groups.

## Lab Evidence: Group Management

The following screenshot demonstrates:

- Creating a user with `adduser`
- Creating a custom group
- Adding a user to a supplementary group
- Verifying group memberships

![Group Management](screenshots/06-02-group-management.png)

## Step 9: Configure a Shared Directory

A shared project directory was created under `/srv`.

```bash
sudo mkdir /srv/projects
```

Ownership was changed:

```bash
sudo chown prince:developers /srv/projects
```

Directory permissions were configured:

```bash
sudo chmod 770 /srv/projects
```

Permission breakdown:

| Permission | Description |
|------------|-------------|
| Owner | Read, Write, Execute |
| Group | Read, Write, Execute |
| Others | No access |

This configuration allows only the owner and members of the `developers` group to access the directory.

## Lab Evidence: Shared Directory Configuration

The following screenshot demonstrates:

- Creating the shared directory
- Changing ownership
- Assigning the developers group
- Configuring directory permissions

![Directory Permissions](screenshots/06-03-directory-permissions.png)
## Step 10: Verify User Access

To confirm that permissions were correctly applied, the session was switched to the `prince` account.

```bash
su - prince
```

The user navigated to the shared directory and created a test file.

```bash
cd /srv/projects

touch project.txt

ls -l
```

The successful creation of the file confirms that the configured permissions allow authorized users to access the shared directory.

## Lab Evidence: Permission Verification

The following screenshot verifies that:

- The user successfully logged in
- The shared directory was accessible
- A new file was created successfully
- The configured permissions functioned as expected

![Permission Verification](screenshots/06-04-user-access-test.png)

# Commands Used

```bash
whoami

id

cat /etc/passwd

awk -F: '$3 >= 1000 {print $1}' /etc/passwd

sudo useradd admin2

id admin2

sudo usermod -aG sudo admin2

groups admin2

sudo adduser prince

id prince

sudo groupadd developers

grep developers /etc/group

sudo usermod -aG developers prince

groups prince

sudo mkdir /srv/projects

sudo chown prince:developers /srv/projects

sudo chmod 770 /srv/projects

su - prince

cd /srv/projects

touch project.txt

ls -l
```

# Key Learning Outcomes

During this chapter I learned how to:

- Identify the current user and inspect user information
- View local user accounts stored in `/etc/passwd`
- Create users using both `useradd` and `adduser`
- Grant administrative privileges using the `sudo` group
- Understand the difference between primary and supplementary groups
- Create custom groups
- Add users to supplementary groups using `usermod -aG`
- Configure ownership and permissions for shared directories
- Verify user access by testing permissions with a non administrative account
- Apply Linux role based access control using users, groups and file permissions
