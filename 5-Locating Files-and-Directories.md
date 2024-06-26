### Locating Files by Name

#### Objectives
- Specify the location of files relative to the current working directory and by absolute location.
- Determine and change the working directory.
- List the contents of directories.

#### Absolute Paths and Relative Paths

The path of a file or directory specifies its unique location in the file system hierarchy. It traverses one or more named subdirectories, delimited by a forward slash (/), until the destination is reached.

##### Important Note
A space character is acceptable as part of a Linux file name. However, spaces are also used by the shell to separate options and arguments on the command line. If you enter a command that includes a file with a space in its name, the shell might misinterpret the command. To avoid this, enclose file names with spaces in quotes.

#### Absolute Paths
An absolute path is a fully qualified name, specifying the exact location in the file system hierarchy. It begins at the root (/) directory and specifies each subdirectory that must be traversed to reach the specific file. An absolute path name starts with a forward slash (/).

**Example:**
- Absolute path for the system message log file: `/var/log/messages`

#### The Current Working Directory and Relative Paths
The working directory, or current working directory, refers to the current location of the user or process.

A relative path identifies a unique file by specifying the path necessary to reach the file from the working directory. A relative path name does not start with a forward slash (/).

**Example:**
- A user in the `/var` directory could refer to the message log file relatively as `log/messages`.

#### Navigating Paths

**Commands:**

- **pwd**: Displays the full path name of the current working directory.
- **ls**: Lists directory contents for the specified directory or the current working directory if no directory is given.
- **cd**: Changes the current working directory for the shell. If no arguments are provided, it changes to the home directory.
  
**Example:**
```sh
[user@host ~]$ pwd
/home/user
[user@host ~]$ cd Videos
[user@host Videos]$ pwd
/home/user/Videos
[user@host Videos]$ cd /home/user/Documents
[user@host Documents]$ pwd
/home/user/Documents
[user@host Documents]$ cd
[user@host ~]$ pwd
/home/user
```

**Creating Files:**
- **touch**: Updates a file's timestamp or creates an empty file if it does not exist.

**Example:**
```sh
[user@host ~]$ touch Videos/blockbuster1.ogg
[user@host ~]$ touch Videos/blockbuster2.ogg
[user@host ~]$ touch Documents/thesis_chapter1.odf
[user@host ~]$ touch Documents/thesis_chapter2.odf
```

**Listing Files:**
- **ls -l**: Long listing format.
- **ls -a**: Includes hidden files.
- **ls -R**: Recursive, includes the contents of all subdirectories.

**Example:**
```sh
[user@host ~]$ ls -l
total 15
drwxr-xr-x. 2 user user 4096 Feb 7 14:02 Desktop
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Documents
drwxr-xr-x. 3 user user 4096 Jan 9 15:00 Downloads
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Music
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Pictures
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Public
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Templates
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Videos
[user@host ~]$ ls -la
total 15
drwx------. 16 user user 4096 Feb 8 16:15 .
drwxr-xr-x. 6 root root 4096 Feb 8 16:13 ..
-rw-------. 1 user user 22664 Feb 8 00:37 .bash_history
-rw-r--r--. 1 user user 18 Jul 9 2013 .bash_logout
-rw-r--r--. 1 user user 176 Jul 9 2013 .bash_profile
-rw-r--r--. 1 user user 124 Jul 9 2013 .bashrc
drwxr-xr-x. 4 user user 4096 Jan 20 14:02 .cache
drwxr-xr-x. 8 user user 4096 Feb 5 11:45 .config
drwxr-xr-x. 2 user user 4096 Feb 7 14:02 Desktop
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Documents
drwxr-xr-x. 3 user user 4096 Jan 25 20:48 Downloads
drwxr-xr-x. 11 user user 4096 Feb 6 13:07 .gnome2
drwx------. 2 user user 4096 Jan 20 14:02 .gnome2_private
-rw-------. 1 user user 15190 Feb 8 09:49 .ICEauthority
drwxr-xr-x. 3 user user 4096 Jan 9 15:00 .local
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Music
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Pictures
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Public
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Templates
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Videos
[user@host ~]$ ls -R
.:
Desktop Documents Downloads Music Pictures Public Templates Videos
./Desktop:
./Documents:
thesis_chapter1.odf thesis_chapter2.odf
./Downloads:
./Music:
./Pictures:
./Public:
./Templates:
./Videos:
blockbuster1.ogg blockbuster2.ogg
```

**Special Directories:**
- **.**: Current directory.
- **..**: Parent directory.

**Navigating Up:**
- **cd ..**: Moves up one level to the parent directory.
- **cd -**: Changes to the previous directory.

**Example:**
```sh
[user@host Videos]$ pwd
/home/user/Videos
[user@host Videos]$ cd .
[user@host Videos]$ pwd
/home/user/Videos
[user@host Videos]$ cd ..
[user@host ~]$ pwd
/home/user
[user@host ~]$ cd ..
[user@host home]$ pwd
/home
[user@host home]$ cd ..
[user@host /]$ pwd
/
[user@host /]$ cd
[user@host ~]$ pwd
/home/user
```

#### References
- **info libc 'file name resolution' (GNU C Library Reference Manual)**
  - Section 11.2.2 File name resolution
- **bash(1), cd(1), ls(1), pwd(1), unicode(7), and utf-8(7) man pages**
- **UTF-8 and Unicode**
  - [UTF-8 and Unicode](http://www.utf-8.com/)
