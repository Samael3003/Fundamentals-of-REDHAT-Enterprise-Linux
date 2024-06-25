## Executing Commands Using the Bash Shell

### Objectives
After completing this section, I should be able to save time running commands from a shell prompt using Bash shortcuts.

### Basic Command Syntax
The GNU Bourne-Again Shell (bash) interprets commands I type. Each command string can have three parts: the command, options (usually beginning with a `-` or `--`), and arguments. Words are separated by spaces. Commands are the names of programs installed on the system, each with its own options and arguments.

When I am ready to execute a command, I press the Enter key. Each command should be typed on a separate line, and the output is displayed before the next shell prompt appears.

Example:
```
[user@host]$ whoami
user
[user@host]$
```

If I want to type more than one command on a single line, I use a semicolon (`;`) as a command separator. The output of both commands will be displayed before the next shell prompt appears.

Example:
```
[user@host]$ command1; command2
```

### Examples of Simple Commands

#### The `date` Command
The `date` command displays the current date and time. It can also be used by the superuser to set the system clock. An argument beginning with a plus sign (`+`) specifies a format string.

Examples:
```
[user@host ~]$ date
Sat Jan 26 08:13:50 IST 2019

[user@host ~]$ date +%R
08:13

[user@host ~]$ date +%x
01/26/2019
```

#### The `passwd` Command
The `passwd` command changes a user's password. I must specify the original password before a change is allowed. By default, `passwd` requires a strong password with lowercase letters, uppercase letters, numbers, and symbols. The superuser can change other users' passwords.

Example:
```
[user@host ~]$ passwd
Changing password for user user.
Current password: old_password
New password: new_password
Retype new password: new_password
passwd: all authentication tokens updated successfully.
```

#### The `file` Command
The `file` command classifies files by type, scanning the beginning of a file's contents.

Examples:
```
[user@host ~]$ file /etc/passwd
/etc/passwd: ASCII text

[user@host ~]$ file /bin/passwd
/bin/passwd: setuid ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=a3637110e27e9a48dced9f38b4ae43388d32d0e4, stripped

[user@host ~]$ file /home
/home: directory
```

### Viewing the Contents of Files

#### The `cat` Command
The `cat` command allows me to create, view, and concatenate files, and redirect contents.

Example to view the contents of `/etc/passwd`:
```
[user@host ~]$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
...output omitted...
```

To display the contents of multiple files:
```
[user@host ~]$ cat file1 file2
Hello World!!
Introduction to Linux commands.
```

#### The `less` Command
The `less` command displays one page of a file at a time, allowing me to scroll with the UpArrow and DownArrow keys. Press `q` to exit.

#### The `head` and `tail` Commands
The `head` command displays the beginning of a file, and the `tail` command displays the end. By default, both display 10 lines but have a `-n` option to specify a different number.

Examples:
```
[user@host ~]$ head /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
...output omitted...

[user@host ~]$ tail -n 3 /etc/passwd
gdm:x:42:42::/var/lib/gdm:/sbin/nologin
gnome-initial-setup:x:977:977::/run/gnome-initial-setup/:/sbin/nologin
avahi:x:70:70:Avahi mDNS/DNS-SD Stack:/var/run/avahi-daemon:/sbin/nologin
```

#### The `wc` Command
The `wc` command counts lines, words, and characters in a file. Options `-l`, `-w`, and `-c` display the number of lines, words, or characters, respectively.

Examples:
```
[user@host ~]$ wc /etc/passwd
 45 102 2480 /etc/passwd

[user@host ~]$ wc -l /etc/passwd ; wc -l /etc/group
45 /etc/passwd
70 /etc/group

[user@host ~]$ wc -c /etc/group /etc/hosts
 966 /etc/group
 516 /etc/hosts
1482 total
```

### Tab Completion
Tab completion allows me to quickly complete commands or file names after typing enough to make them unique. If not unique, pressing Tab twice displays all commands starting with the typed characters.

Example:
```
[user@host ~]$ pas<Tab><Tab>
passwd paste pasuspender

[user@host ~]$ pass<Tab>
passwd
```

### Continuing a Long Command on Another Line
For readability, I can use a backslash (`\`) to continue a long command on another line. The shell moves to a new command line without executing until I finish.

Example:
```
[user@host]$ head -n 3 \
/usr/share/dict/words \
/usr/share/dict/linux.words
```

### Command History
The `history` command lists previously executed commands. The exclamation point (`!`) expands previous commands without retyping them.

Examples:
```
[user@host ~]$ history
 ...output omitted...
 23 clear
 24 who
 25 pwd
 26 ls /etc
 27 uptime
 28 ls -l
 29 date
 30 history

[user@host ~]$ !ls
ls -l
...output omitted...

[user@host ~]$ !26
ls /etc
...output omitted...
```

I can navigate through previous commands using the arrow keys: UpArrow for the previous command, DownArrow for the next, and LeftArrow and RightArrow to move within a command. Using `Esc+.` or `Alt+.` inserts the last word of the previous command at the cursor's location. Repeating this key combination cycles through earlier commands.

### Editing the Command Line
Bash's command-line editing feature allows me to use text editor commands within the current command. Some useful shortcuts include:

- **Ctrl+A**: Jump to the beginning of the command line.
- **Ctrl+E**: Jump to the end of the command line.
- **Ctrl+U**: Clear from the cursor to the beginning of the command line.
- **Ctrl+K**: Clear from the cursor to the end of the command line.
- **Ctrl+LeftArrow**: Jump to the beginning of the previous word.
- **Ctrl+RightArrow**: Jump to the end of the next word.
- **Ctrl+R**: Search the history list for a pattern.

These shortcuts enhance efficiency and ease of use when working in the shell.

### References
- `bash(1)`, `date(1)`, `file(1)`, `cat(1)`, `more(1)`, `less(1)`, `head(1)`, `passwd(1)`, `tail(1)`, and `wc(1)` man pages.
