### The Linux File System Hierarchy

#### Objectives
- Understand how Linux organizes files.
- Identify the purposes of various directories in the file-system hierarchy.

#### The File-system Hierarchy
Linux organizes files into a single inverted tree of directories, known as the file-system hierarchy. The root of this tree is at the top, and it branches down into directories and subdirectories.

#### Important Directories in Red Hat Enterprise Linux 8

**/**  
- The root directory at the top of the file-system hierarchy.

**/usr**  
- Contains installed software, shared libraries, include files, and read-only program data.
  - **/usr/bin**: User commands.
  - **/usr/sbin**: System administration commands.
  - **/usr/local**: Locally customized software.

**/etc**  
- Contains configuration files specific to the system.

**/var**  
- Holds variable data specific to the system that should persist between boots, such as databases, log files, cache directories, printer-spooled documents, and website content.

**/run**  
- Stores runtime data for processes started since the last boot, including process ID files and lock files. This content is recreated on reboot.

**/home**  
- Contains home directories for regular users, where they store personal data and configuration files.

**/root**  
- The home directory for the administrative superuser, root.

**/tmp**  
- A world-writable space for temporary files. Files not accessed, changed, or modified for 10 days are deleted automatically. Another temporary directory, **/var/tmp**, holds files that are deleted automatically if not accessed, changed, or modified for more than 30 days.

**/boot**  
- Contains files needed to start the boot process.

**/dev**  
- Contains special device files used by the system to access hardware.

#### Notes on Directory Contents
- **Static content**: Remains unchanged until explicitly edited or reconfigured.
- **Dynamic or variable content**: May be modified or appended by active processes.
- **Persistent content**: Remains after a reboot, like configuration settings.
- **Runtime content**: Process- or system-specific content deleted by a reboot.

#### Important
In Red Hat Enterprise Linux 7 and later, certain directories in **/** have identical contents to their counterparts in **/usr**:
- **/bin** and **/usr/bin**
- **/sbin** and **/usr/sbin**
- **/lib** and **/usr/lib**
- **/lib64** and **/usr/lib64**

These directories in **/** are symbolic links to the corresponding directories in **/usr**. This was not the case in earlier versions of Red Hat Enterprise Linux, where these were distinct directories with different sets of files.

#### References
- **hier(7) man page**
- **The UsrMove feature page from Fedora 17**: [UsrMove](https://fedoraproject.org/wiki/Features/UsrMove)
