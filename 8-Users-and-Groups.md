## Users and Groups

### Objectives
After completing this section, you should be able to:
- Describe the purpose of users and groups on a Linux system.

### What is a User?
A user account provides security boundaries between different people and programs that can run commands. Users have usernames for human identification and User IDs (UIDs) for system identification. Each user can have a password for authentication, and every process and file on the system is associated with a specific user, which helps enforce access control.

#### Types of User Accounts
1. **Superuser**: 
   - Name: root
   - UID: 0
   - Full access to the system.

2. **System Users**:
   - Used by processes providing supporting services.
   - Non-privileged accounts.
   - Do not interactively log in using these accounts.

3. **Regular Users**:
   - Used for day-to-day work.
   - Limited access to the system.

#### Commands for User Information
- View current user information:
  ```bash
  [user01@host ~]$ id
  ```
  Output:
  ```plaintext
  uid=1000(user01) gid=1000(user01) groups=1000(user01)
  ```

- View another user’s information:
  ```bash
  [user01@host]$ id user02
  ```
  Output:
  ```plaintext
  uid=1002(user02) gid=1001(user02) groups=1001(user02)
  ```

#### Viewing File and Process Information
- View file owner:
  ```bash
  [user01@host ~]$ ls -l file1
  ```
  Output:
  ```plaintext
  -rw-rw-r--. 1 user01 user01 0 Feb 5 11:10 file1
  ```

- View directory owner:
  ```bash
  [user01@host]$ ls -ld dir1
  ```
  Output:
  ```plaintext
  drwxrwxr-x. 2 user01 user01 6 Feb 5 11:10 dir1
  ```

- View process information:
  ```bash
  [user01@host]$ ps -au
  ```
  Output:
  ```plaintext
  USER     PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
  root     777  0.0  0.0 225752  1496 tty1     Ss+  11:03   0:00 /sbin/agetty -o -
  root     780  0.0  0.1 225392  2064 ttyS0    Ss+  11:03   0:00 /sbin/agetty -o -
  user01  1207  0.0  0.2 234044  5104 pts/0    Ss   11:09   0:00 -bash
  user01  1319  0.0  0.2 266904  3876 pts/0    R+   11:33   0:00 ps au
  ```

#### User Account Information in /etc/passwd
Example of a line in `/etc/passwd`:
```plaintext
user01:x:1000:1000:User One:/home/user01:/bin/bash
```
Fields:
1. **Username**: `user01`
2. **Password Placeholder**: `x` (password stored in `/etc/shadow`)
3. **UID**: `1000`
4. **GID**: `1000`
5. **Real Name**: `User One`
6. **Home Directory**: `/home/user01`
7. **Default Shell**: `/bin/bash`

### What is a Group?
A group is a collection of users that need to share access to files and other resources. Groups simplify access control management. Groups are identified by group names and Group IDs (GIDs).

#### Group Information in /etc/group
Example of a line in `/etc/group`:
```plaintext
group01:x:10000:user01,user02,user03
```
Fields:
1. **Group Name**: `group01`
2. **Password Placeholder**: `x`
3. **GID**: `10000`
4. **Members**: `user01,user02,user03`

#### Primary and Supplementary Groups
- **Primary Group**: The group listed by GID in the `/etc/passwd` file. It owns new files created by the user.
- **Supplementary Groups**: Additional groups a user is a member of, listed in the `/etc/group` file. 

Example:
```plaintext
uid=1003(user03) gid=1003(user03) groups=1003(user03),10(wheel),10000(group01)
```
- Primary group: `user03`
- Supplementary groups: `wheel`, `group01`

### References
- `id(1)`, `passwd(5)`, and `group(5)` man pages
- `info libc` (GNU C Library Reference Manual), Section 30: Users and Groups
