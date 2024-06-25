## Accessing the Command Line

### Objectives
After completing this section, I should be able to log in to a Linux system and run simple commands using the shell.

### Introduction to the Bash Shell
A command line is a text-based interface that I can use to input instructions to a computer system. The Linux command line is provided by a program called the shell. There are various shell options, but most users, including myself, stick with the current default.

The default shell for users in Red Hat Enterprise Linux is the GNU Bourne-Again Shell (bash). Bash is an improved version of the Bourne Shell (sh), a successful shell used on UNIX-like systems.

When I use the shell interactively, it displays a string when waiting for a command from me, called the shell prompt. When I start a shell as a regular user, the default prompt ends with a `$` character:
```
[user@host ~]$
```
If the shell is running as the superuser, root, the `$` character is replaced by a `#` character:
```
[root@host ~]#
```
Using bash to execute commands is powerful. The bash shell provides a scripting language that can automate tasks and simplify or make possible operations that are hard to accomplish with graphical tools.

**Note:** The bash shell is similar to the command-line interpreter found in recent versions of Microsoft Windows, `cmd.exe`, although bash has a more sophisticated scripting language. It is also similar to Windows PowerShell in Windows 7 and later. As an administrator using the Apple Mac's Terminal utility, I will note that bash is the default shell in macOS.

### Shell Basics
Commands entered at the shell prompt have three basic parts:
- **Command to run:** The name of the program to run.
- **Options:** Adjust the behavior of the command, typically starting with one or two dashes (e.g., `-a` or `--all`).
- **Arguments:** Targets of the command.

For example, the command `usermod -L user01` has:
- **Command:** `usermod`
- **Option:** `-L`
- **Argument:** `user01`

Many commands have a `--help` option that displays a usage message and the list of available options.

### Logging in to a Local Computer
To run the shell, I need to log in to the computer on a terminal, which is a text-based interface for entering commands and viewing output.

#### Physical Console
The physical console of a Linux machine has multiple virtual consoles, each supporting independent login sessions. I can switch between them by pressing `Ctrl+Alt` and a function key (F1 through F6).

#### Graphical Environment
In Red Hat Enterprise Linux 8, the graphical login screen runs on the first virtual console (tty1). Logging in starts a graphical environment on the first unused virtual console, usually tty2. Logging out of a graphical environment switches back to the graphical login screen on tty1.

#### Headless Server
A headless server lacks a keyboard and display. Access is typically through a networked console server or over the network via SSH.

### Logging in over the Network
I can use Secure Shell (SSH) to get a shell prompt on a remote system. The OpenSSH command-line program `ssh` is commonly used.

Example login:
```
[user@host ~]$ ssh remoteuser@remotehost
remoteuser@remotehost's password: password
[remoteuser@remotehost ~]$
```
SSH encrypts the connection for secure communication. Some systems use public key authentication instead of passwords.

Example using a private key file:
```
[user@host ~]$ ssh -i mylab.pem remoteuser@remotehost
[remoteuser@remotehost ~]$
```
I need to ensure the private key file is readable only by its owner:
```
chmod 600 mylab.pem
```
The first time I log in to a new machine, I will see a warning about the host's authenticity. I need to confirm with `yes` to save the host key for future reference.

### Logging Out
To end a shell session, I can use the `exit` command or press `Ctrl+D`.

Example logging out of an SSH session:
```
[remoteuser@remotehost ~]$ exit
logout
Connection to remotehost closed.
[user@host ~]$
```

### References
- `intro(1)`, `bash(1)`, `console(4)`, `pts(4)`, `ssh(1)`, and `ssh-keygen(1)` man pages.
- For more information on OpenSSH and public key authentication, refer to the Red Hat Enterprise Linux 8 Securing Networks guide at:
  [Red Hat Enterprise Linux 8 Securing Networks](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/securing_networks/index#using-secure-communications-between-two-systems-with-openssh_securing-networks)

**Note:** Instructions on reading man pages and other online help documentation are included at the end of the next section.
