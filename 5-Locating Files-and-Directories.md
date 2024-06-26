drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Public
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Templates
drwxr-xr-x. 2 user user 4096 Jan 9 15:00 Videos
[user@host ~]$
The two special directories at the top of the listing refer to the current directory (.) and the parent
directory (..). These special directories exist in every directory on the system. You will discover
their usefulness when you start using file management commands.
Important
File names beginning with a dot (.) indicate hidden files; you cannot see them in the
normal view using ls and other commands. This is not a security feature. Hidden
files keep necessary user configuration files from cluttering home directories. Many
commands process hidden files only with specific command-line options, preventing
one user's configuration from being accidentally copied to other directories or users.
To protect file contents from improper viewing requires the use of file permissions.
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
[user@host ~]$
The cd command has many options. A few are so useful as to be worth practicing early and using
often. The command cd - changes to the previous directory; where the user was previously to
the current directory. The following example illustrates this behavior, alternating between two
directories, which is useful when processing a series of similar tasks.
[user@host ~]$ cd Videos
[user@host Videos]$ pwd
/home/user/Videos
[user@host Videos]$ cd /home/user/Documents
[user@host Documents]$ pwd
/home/user/Documents
46 RH066-RHEL8-en-1-cef4e50
Chapter 3 | Managing Files From the Command Line
[user@host Documents]$ cd -
[user@host Videos]$ pwd
/home/user/Videos
[user@host Videos]$ cd -
[user@host Documents]$ pwd
/home/user/Documents
[user@host Documents]$ cd -
[user@host Videos]$ pwd
/home/user/Videos
[user@host Videos]$ cd
[user@host ~]$
The cd .. command uses the .. hidden directory to move up one level to the parent directory,
without needing to know the exact parent name. The other hidden directory (.) specifies the
current directory on commands in which the current location is either the source or destination
argument, avoiding the need to type out the directory's absolute path name.
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
[user@host ~]$
References
info libc 'file name resolution' (GNU C Library Reference Manual)
• Section 11.2.2 File name resolution
bash(1), cd(1), ls(1), pwd(1), unicode(7), and utf-8(7) man pages
UTF-8 and Unicode
http://www.utf-8.com/
