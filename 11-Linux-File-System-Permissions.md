## Linux File System Permissions

### Objectives
After completing this section, you should be able to list file-system permissions on files and directories and interpret the effect of those permissions on access by users and groups.

### Linux File-system Permissions Overview

Linux file permissions control access to files and directories. Permissions are applied to three categories of users:
- **User (owner)**
- **Group**
- **Other (everyone else)**

Each category can have different permissions, and the most specific permissions take precedence:
- **User permissions** override **group permissions**, which override **other permissions**.

### Permissions and Their Effects

Three types of permissions apply to files and directories:
- **Read (r)**: Allows reading the contents of files or listing the contents of directories.
- **Write (w)**: Allows modifying files or adding/deleting files within directories.
- **Execute (x)**: Allows running files as commands or changing into directories with `cd`.

#### Effects on Files and Directories

| Permission | Effect on Files | Effect on Directories |
|------------|-----------------|-----------------------|
| **Read (r)** | File contents can be read. | Directory contents (file names) can be listed. |
| **Write (w)** | File contents can be changed. | Files can be created or deleted within the directory. |
| **Execute (x)** | Files can be executed as commands. | The directory can be changed into with `cd`. |

**Note:**
- Users typically need both read and execute permissions on directories for full read-only access.
- Write permission on a directory allows deletion of files, regardless of the file's own permissions.
- Permissions on directories can block access depending on how restrictive they are.

### Viewing File and Directory Permissions and Ownership

- **List Detailed Information About Files and Directories:**
  ```bash
  ls -l
  ```
  - Example:
    ```bash
    [user@host ~]$ ls -l test
    -rw-rw-r--. 1 student student 0 Feb 8 17:36 test
    ```

- **List Detailed Information About a Directory:**
  ```bash
  ls -ld directory_name
  ```
  - Example:
    ```bash
    [user@host ~]$ ls -ld /home
    drwxr-xr-x. 5 root root 4096 Jan 31 22:00 /home
    ```

### Understanding the Output of `ls -l`

- **File Type:**
  - `-` : Regular file
  - `d` : Directory
  - `l` : Symbolic link
  - Other characters (e.g., `b`, `c`, `p`, `s`) represent special files.

- **Permissions:**
  - Three sets of three characters each, representing permissions for user, group, and others.
  - Example:
    ```bash
    -rw-rw-r--. 1 student student 0 Feb 8 17:36 test
    ```
    - **User (student):** `rw-` (read, write)
    - **Group (student):** `rw-` (read, write)
    - **Others:** `r--` (read)

### Examples of Permission Effects

#### Example User Group Memberships

| User       | Group Memberships        |
|------------|---------------------------|
| operator1  | operator1, consultant1    |
| database1  | database1, consultant1    |
| database2  | database2, operator2      |
| contractor1| contractor1, operator2    |

#### Directory Listing Example

```bash
[database1@host dir]$ ls -la
total 24
drwxrwxr-x. 2 database1 consultant1 4096 Apr 4 10:23 .
drwxr-xr-x. 10 root root 4096 Apr 1 17:34 ..
-rw-rw-r--. 1 operator1 operator1 1024 Apr 4 11:02 lfile1
-rw-r--rw-. 1 operator1 consultant1 3144 Apr 4 11:02 lfile2
-rw-rw-r--. 1 database1 consultant1 10234 Apr 4 10:14 rfile1
-rw-r-----. 1 database1 consultant1 2048 Apr 4 10:18 rfile2
```

- **`.` (dir itself)**: `drwxrwxr-x` (owned by database1, group consultant1)
- **`..` (parent directory)**: `drwxr-xr-x` (owned by root, group root)
- **`lfile1`**: `-rw-rw-r--` (owned by operator1, group operator1)
- **`lfile2`**: `-rw-r--rw-` (owned by operator1, group consultant1)
- **`rfile1`**: `-rw-rw-r--` (owned by database1, group consultant1)
- **`rfile2`**: `-rw-r-----` (owned by database1, group consultant1)

### Notes

- Linux file permissions are different from NTFS permissions on Windows.
- Permissions on a directory are not inherited by files/subdirectories within it.
- The root user has full control over all files, but access can be restricted by SELinux policies.

### References

- `ls(1)` man page
