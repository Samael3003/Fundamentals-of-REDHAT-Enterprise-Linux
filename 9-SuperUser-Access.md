## Gaining Superuser Access

### Objectives

After completing this section, you will be able to:
- Switch to the superuser account to manage a Linux system.
- Grant other users superuser access through the `sudo` command.

### The Superuser

- The **root** user in Red Hat Enterprise Linux is the superuser, having full control over the system.
- Root can override normal privileges, install/remove software, and manage system files and directories.
- Root has the power to control most devices, except for removable devices which can be managed by normal users.
- Root’s privileges carry responsibility; misuse can damage the system or compromise security.
- System administrators are encouraged to log in as normal users and escalate privileges to root only when needed, avoiding direct login as root.

### Switching Users with `su`

- The `su` command allows switching to a different user account.
- Running `su` prompts for the password of the target user account.
- Running `su` as root does not require the target user's password.
- `su` starts a non-login shell, whereas `su -` starts a login shell, setting up the shell environment as if it were a new login for that user.
- For most administrative tasks, `su -` is recommended to set up the target user's normal environment.

**Examples:**
```bash
[user01@host ~]$ su - user02
Password:
[user02@host ~]$

[user01@host ~]$ su -
Password:
[root@host ~]#
```

### Running Commands with `sudo`

- `sudo` allows users to run commands as another user, typically root, without needing the target user's password.
- Users authenticate with their own password.
- `sudo` can be configured to allow specific users to run any command or only certain commands as root.
- The `sudo` configuration is managed via `/etc/sudoers`, which should be edited using the `visudo` command to prevent conflicts.

**Example:**
```bash
[user01@host ~]$ sudo usermod -L user02
[sudo] password for user01:

[user02@host ~]$ sudo tail /var/log/secure
[sudo] password for user02:
user02 is not in the sudoers file. This incident will be reported.
```

- All commands executed with `sudo` are logged to `/var/log/secure`.

### Gaining an Interactive Root Shell with `sudo`

- Use `sudo su -` to get an interactive root shell.
- `sudo -i` can also switch to the root account and run the default shell with associated login scripts.
- `sudo -s` runs the shell without running login scripts.

**Example:**
```bash
[ec2-user@host ~]$ sudo -i
[sudo] password for ec2-user:
[root@host ~]#
```

### Configuring `sudo`

- The main configuration file for `sudo` is `/etc/sudoers`.
- `%wheel ALL=(ALL) ALL` grants sudo access to all members of the wheel group.
- Adding files to `/etc/sudoers.d` allows for modular sudo configuration.

**Example:**
To enable full `sudo` access for `user01`, create `/etc/sudoers.d/user01` with:
```
user01 ALL=(ALL) ALL
```

To allow a user to run commands without entering a password:
```
ansible ALL=(ALL) NOPASSWD:ALL
```

- This configuration is useful for automation and provisioning systems but requires careful security considerations.

**Note:**
To make `sudo -i` behave more like `su -`, edit `/etc/sudoers` with `visudo`:
```bash
Defaults secure_path = /sbin:/bin:/usr/sbin:/usr/bin
Defaults>root secure_path = /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin
```

### References

- `su(1)`, `sudo(8)`, `visudo(8)`, `sudoers(5)` man pages
- `info libc persona` (GNU C Library Reference Manual)
