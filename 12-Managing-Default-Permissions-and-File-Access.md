## Managing Default Permissions and File Access

### Objectives
After completing this section, you should be able to:
- Control the default permissions of new files created by users.
- Explain the effect of special permissions.
- Use special permissions and default permissions to set the group owner of files created in a particular directory.

### Special Permissions
Special permissions provide additional access-related features over the basic permissions of user, group, and other.

#### Effects of Special Permissions on Files and Directories

| Special Permission | Effect on Files                           | Effect on Directories                                                                            |
|---------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------|
| `u+s` (setuid)      | File executes as the user that owns the file, not the user that ran the file. | No effect.                                                                                       |
| `g+s` (setgid)      | File executes as the group that owns the file.                | Files newly created in the directory inherit the group owner of the directory.                   |
| `o+t` (sticky)      | No effect.                                | Users with write access to the directory can only remove files that they own.                    |

#### Examples:
- **Setuid (`u+s`)**: When set on an executable file, the file runs with the permissions of the file's owner.
  - Example: `passwd` command:
    ```bash
    ls -l /usr/bin/passwd
    -rwsr-xr-x. 1 root root 35504 Jul 16 2010 /usr/bin/passwd
    ```
- **Setgid (`g+s`)**: When set on a directory, new files in the directory inherit the group ownership from the directory.
  - Example: `/run/log/journal` directory:
    ```bash
    ls -ld /run/log/journal
    drwxr-sr-x. 3 root systemd-journal 60 May 18 09:15 /run/log/journal
    ```
- **Sticky bit (`o+t`)**: Only the file owner (or root) can delete files in the directory.
  - Example: `/tmp` directory:
    ```bash
    ls -ld /tmp
    drwxrwxrwt. 39 root root 4096 Feb 8 20:52 /tmp
    ```

#### Setting Special Permissions

- **Symbolically**: `setuid` = `u+s`, `setgid` = `g+s`, `sticky` = `o+t`
- **Numerically (fourth preceding digit)**: `setuid` = 4, `setgid` = 2, `sticky` = 1

##### Examples:
- **Add the setgid bit on a directory**:
  ```bash
  chmod g+s directory
  ```
- **Set the setgid bit and add read/write/execute permissions for user and group, with no access for others, on a directory**:
  ```bash
  chmod 2770 directory
  ```

### Default File Permissions
New files and directories are assigned initial permissions, influenced by whether the item is a regular file or a directory, and by the current `umask`.

#### Default Permissions:
- **Directories**: Start with permissions `0777` (drwxrwxrwx).
- **Regular files**: Start with permissions `0666` (-rw-rw-rw-). Execute permission must be explicitly added.

#### Umask
The `umask` sets a bitmask that clears permissions on new files and directories created by a process. 

- **Default umask values**:
  - `0002`: Clears the write bit for others.
  - `0077`: Clears all group and other permissions.

#### Viewing and Setting Umask:
- **View current umask**:
  ```bash
  umask
  ```
- **Set umask**:
  ```bash
  umask 002
  ```

#### Examples:
- **Default umask 0002**:
  ```bash
  umask
  0002
  touch default.txt
  ls -l default.txt
  -rw-rw-r--. 1 user user 0 May 9 01:54 default.txt
  mkdir default
  ls -ld default
  drwxrwxr-x. 2 user user 0 May 9 01:54 default
  ```
- **Umask set to 0**:
  ```bash
  umask 0
  touch zero.txt
  ls -l zero.txt
  -rw-rw-rw-. 1 user user 0 May 9 01:54 zero.txt
  mkdir zero
  ls -ld zero
  drwxrwxrwx. 2 user user 0 May 9 01:54 zero
  ```
- **Umask set to 007**:
  ```bash
  umask 007
  touch seven.txt
  ls -l seven.txt
  -rw-rw----. 1 user user 0 May 9 01:55 seven.txt
  mkdir seven
  ls -ld seven
  drwxrwx---. 2 user user 0 May 9 01:54 seven
  ```
- **Umask set to 027**:
  ```bash
  umask 027
  touch two-seven.txt
  ls -l two-seven.txt
  -rw-r-----. 1 user user 0 May 9 01:55 two-seven.txt
  mkdir two-seven
  ls -ld two-seven
  drwxr-x---. 2 user user 0 May 9 01:54 two-seven
  ```

#### Changing Default Umask for All Users
- **System-wide umask configuration**: Modify `/etc/profile.d/local-umask.sh`.

```bash
[root@host ~]# cat /etc/profile.d/local-umask.sh
# Overrides default umask configuration
if [ $UID -gt 199 ] && [ "`id -gn`" = "`id -un`" ]; then
 umask 007
else
 umask 022
fi
```

- To set umask for all users to `022`:
```bash
# Overrides default umask configuration
umask 022
```

**Note**: For changes to take effect globally, users need to log out and log back in.

### References
- `bash(1)`, `ls(1)`, `chmod(1)`, and `umask(1)` man pages

This guide provides the necessary commands and examples for managing default file permissions and special permissions in a Linux environment.
