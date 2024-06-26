## Managing Local Group Accounts

### Objectives

After completing this section, you should be able to:
- Create, modify, and delete local group accounts.

### Creating Groups from the Command Line

- **Create a New Group:**
  ```bash
  groupadd groupname
  ```
  - Uses the next available GID from the range specified in the `/etc/login.defs` file.

- **Specify a GID for the Group:**
  ```bash
  groupadd -g GID groupname
  ```
  - Example:
    ```bash
    sudo groupadd -g 10000 group01
    tail /etc/group
    ```

**Note:**
- Automatic creation of user private groups (GID 1000+) means it is recommended to set aside a range of GIDs for supplementary groups to avoid collision with system groups (GID 0-999).

- **Create a System Group:**
  ```bash
  groupadd -r groupname
  ```
  - Uses a GID from the range of valid system GIDs listed in `/etc/login.defs`.
  - Example:
    ```bash
    sudo groupadd -r group02
    tail /etc/group
    ```

### Modifying Existing Groups from the Command Line

- **Change Group Name:**
  ```bash
  groupmod -n newgroupname oldgroupname
  ```
  - Example:
    ```bash
    sudo groupmod -n group0022 group02
    tail /etc/group
    ```

- **Change GID:**
  ```bash
  groupmod -g newGID groupname
  ```
  - Example:
    ```bash
    sudo groupmod -g 20000 group0022
    tail /etc/group
    ```

### Deleting Groups from the Command Line

- **Remove a Group:**
  ```bash
  groupdel groupname
  ```
  - Example:
    ```bash
    sudo groupdel group0022
    ```

**Note:**
- You cannot remove a group if it is the primary group of any existing user.
- Check all file systems to ensure that no files remain on the system that are owned by the group.

### Changing Group Membership from the Command Line

- **Change a User's Primary Group:**
  ```bash
  usermod -g groupname username
  ```
  - Example:
    ```bash
    id user02
    sudo usermod -g group01 user02
    id user02
    ```

- **Add a User to a Supplementary Group:**
  ```bash
  usermod -aG groupname username
  ```
  - Example:
    ```bash
    id user03
    sudo usermod -aG group01 user03
    id user03
    ```

**Important:**
- The `-a` option makes `usermod` function in append mode. Without `-a`, the user will be removed from any of their current supplementary groups that are not included in the `-G` option's list.

### References

- `group(5)`, `groupadd(8)`, `groupdel(8)`, and `usermod(8)` man pages
