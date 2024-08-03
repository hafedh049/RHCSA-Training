Certainly! Here's a comprehensive list of commands and files associated with user and group management, including permissions and special permissions, as well as configuration files and utilities.

### **Commands**

#### **User Management**

- **useradd**: Add a new user.
  ```bash
  useradd [options] username
  ```
  Common options:
  - `-c`: Comment field.
  - `-d`: Home directory.
  - `-e`: Account expiration date.
  - `-g`: Initial group.
  - `-G`: Additional groups.
  - `-m`: Create home directory.
  - `-b`: Specify his base directory.
  - `-M`: Don't create his home directory.
  - `-s`: Login shell.

- **usermod**: Modify an existing user.
  ```bash
  usermod [options] username
  ```
  Common options:
  - `-c`: New comment.
  - `-d`: New home directory.
  - `-e`: New expiration date.
  - `-g`: New primary group.
  - `-G`: New supplementary group.
  - `-aG`: Append new supplementary group.
  - `-l`: New login name.
  - `-L`: Lock user account.
  - `-s`: New login shell.
  - `-U`: Unlock user account.

- **userdel**: Delete a user account.
  ```bash
  userdel [options] username
  ```
  Common options:
  - `-r`: Remove home directory and mail spool.
  - `-f`: force.

#### **Group Management**

- **groupadd**: Add a new group.
  ```bash
  groupadd [options] groupname
  ```
  Common options:
  - `-g`: GID.
  - `-r`: Create a system group.

- **groupmod**: Modify an existing group.
  ```bash
  groupmod [options] groupname
  ```
  Common options:
  - `-g`: New GID.
  - `-n`: New group name.

- **groupdel**: Delete a group.
  ```bash
  groupdel groupname
  ```

#### **Password Management**

- **passwd**: Change user password.
  ```scss
  passwd [options] [username]
  ```
  Common options:
  - `-d`: Delete password (make it empty).
  - `-l`: Lock password.
  - `-u`: Unlock password.

- **chpasswd**: Change passwords in batch.
  ```bash
  chpasswd [options]
  ```
  Common options:
  - `-e`: Entries are already encrypted.
  - `-m`: Use MD5 encryption.

- **chage**: Change user password expiry information.
  ```bash
  chage [options] username
  ```
  Common options:
  - `-d`: Last day password was changed.
  - `-E`: Expiration date.
  - `-I`: Inactive days.
  - `-l`: List account aging information.
  - `-m`: Minimum days between changes.
  - `-M`: Maximum days between changes.
  - `-W`: Warning days.

#### **Permissions and Special Permissions**

- **chmod**: Change file mode bits.
  ```bash
  chmod [options] mode file
  ```
  Common options:
  - `-R`: Recursive.

- **chown**: Change file owner and group.
  ```bash
  chown [options] owner[:group] file
  ```
  Common options:
  - `-R`: Recursive.

- **chgrp**: Change group ownership.
  ```bash
  chgrp [options] group file
  ```
  Common options:
  - `-R`: Recursive.

- **setfacl**: Set file access control lists.
  ```bash
  setfacl [options] acl_spec file
  ```
  Common options:
  - `-m`: Modify ACL.
  - `-x`: Remove ACL.
  - `-R`: Recursive.

- **getfacl**: Get file access control lists.
  ```bash
  getfacl [options] file
  ```

### **Configuration Files**

#### **User and Group Information**

- **/etc/passwd**: User account information.
  ```
  username:x:UID:GID:comment:home_directory:shell
  ```

- **/etc/shadow**: Secure user account information.
  ```
  username:password:last_change:min:max:warn:inactive:expire
  ```

- **/etc/group**: Group account information.
  ```
  groupname:x:GID:member1,member2,...
  ```

- **/etc/gshadow**: Secure group account information.
  ```
  groupname:password:group_admins:group_members
  ```

#### **User and Group Defaults**

- **/etc/login.defs**: Shadow password suite configuration.
  - Defines the site-specific configuration for the shadow password suite.

- **/etc/skel/**: Directory for default user files.
  - Contains files and directories that are copied to the new user's home directory when the user is created.

- **/etc/default/useradd**: Default values for `useradd`.
  - Defines default values used by `useradd` when creating new users.

#### **Sudo Configuration**

- **/etc/sudoers**: Sudo configuration file.
  - Controls which users can run what commands as which other users.

- **/etc/sudoers.d/username**: Additional sudoers configuration for a specific user.
  - Can be used to define specific sudo rules for individual users.

#### **Examples**

**Example: Add a New User**

```bash
sudo useradd -m -s /bin/bash newuser
sudo passwd newuser
```

**Example: Modify an Existing User**

```bash
sudo usermod -aG sudo newuser
sudo usermod -d /new/home/directory newuser
```

**Example: Delete a User and Their Home Directory**

```bash
sudo userdel -rf newuser
```

**Example: Add a New Group**

```bash
sudo groupadd newgroup
```

**Example: Modify an Existing Group**

```bash
sudo groupmod -n newgroupname oldgroupname
```

**Example: Delete a Group**

```bash
sudo groupdel newgroup
```

**Example: Change File Ownership**

```bash
sudo chown user:group /path/to/file
```

**Example: Change File Permissions**

```bash
sudo chmod 755 /path/to/file
```

**Example: Set ACLs**

```bash
sudo setfacl -m u:username:rwx /path/to/file
sudo getfacl /path/to/file
```

**Example: Change Password Expiry Information**

```bash
sudo chage -M 90 username
```

**Example: Configure `/etc/sudoers.d/username`**

1. **Create the file:**

   ```bash
   sudo nano /etc/sudoers.d/username
   ```

2. **Add the following line to grant sudo privileges without a password:**

   ```scss
   username ALL=(ALL) NOPASSWD:ALL
   ```

3. **Save and exit the file.**
### **User Management Examples**

#### **Add a New User**

Create a new user `newuser` with a home directory and set their shell to `/bin/bash`.

```bash
sudo useradd -m -s /bin/bash newuser
sudo passwd newuser
```

#### **Modify an Existing User**

Add `newuser` to the `sudo` group.

```bash
sudo usermod -aG sudo newuser
```

Change the home directory of `newuser` to `/new/home/directory`.

```bash
sudo usermod -d /new/home/directory newuser
```

#### **Delete a User and Their Home Directory**

Delete `newuser` and remove their home directory.

```bash
sudo userdel -r newuser
```

### **Group Management Examples**

#### **Add a New Group**

Create a new group `newgroup`.

```bash
sudo groupadd newgroup
```

#### **Modify an Existing Group**

Rename the group `oldgroupname` to `newgroupname`.

```bash
sudo groupmod -n newgroupname oldgroupname
```

#### **Delete a Group**

Delete the group `newgroup`.

```bash
sudo groupdel newgroup
```

### **Password Management Examples**

#### **Change User Password**

Change the password for `newuser`.

```bash
sudo passwd newuser
```

#### **Batch Change Passwords**

Use `chpasswd` to change passwords for multiple users.

```bash
echo "newuser:newpassword" | sudo chpasswd
```

#### **Change Password Expiry Information**

Set the maximum number of days between password changes to 90 for `username`.

```bash
sudo chage -M 90 username
```

List account aging information for `username`.

```bash
sudo chage -l username
```

### **Permissions and Special Permissions Examples**

#### **Change File Ownership**

Change the owner and group of `/path/to/file` to `user` and `group`.

```bash
sudo chown user:group /path/to/file
```

#### **Change File Permissions**

Set the permissions of `/path/to/file` to `755`.

```bash
sudo chmod 755 /path/to/file
```

#### **Set Access Control Lists (ACLs)**

Set ACLs to grant `username` read, write, and execute permissions on `/path/to/file`.

```bash
sudo setfacl -m u:username:rwx /path/to/file
```

Retrieve ACLs for `/path/to/file`.

```bash
sudo getfacl /path/to/file
```

### **Special Permissions Examples**

#### **Set the SUID Bit**

Set the SUID bit on `/path/to/program` to allow it to be executed with the permissions of its owner.

```bash
sudo chmod u+s /path/to/program
```

#### **Set the SGID Bit**

Set the SGID bit on `/path/to/directory` to ensure that new files and subdirectories inherit the group ID.

```bash
sudo chmod g+s /path/to/directory
```

#### **Set the Sticky Bit**

Set the sticky bit on `/path/to/directory` to restrict file deletion to the owner.

```bash
sudo chmod +t /path/to/directory
```

### **Configuration Files Examples**

#### **/etc/passwd**

Example entry:

```scss
newuser:x:1001:1001:New User,,,:/home/newuser:/bin/bash
```

#### **/etc/shadow**

Example entry:

```scss
newuser:$6$randomsalt$hashedpassword:18496:0:99999:7:::
```

#### **/etc/group**

Example entry:

```scss
newgroup:x:1001:
```

#### **/etc/gshadow**

Example entry:

```scss
newgroup:!::
```

#### **/etc/login.defs**

Example content:

```scss
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_MIN_LEN    5
PASS_WARN_AGE   7
```

#### **/etc/skel/**

Files and directories in `/etc/skel/` are copied to new users' home directories. For example, if `/etc/skel/` contains a `.bashrc`, every new user will have a `.bashrc` in their home directory.

### **Sudo Configuration Examples**

#### **/etc/sudoers**

Edit the sudoers file using `visudo`.

```bash
sudo visudo
```

Add a line to allow `newuser` to execute all commands without a password.

```plaintext
newuser ALL=(ALL) NOPASSWD:ALL
```

#### **/etc/sudoers.d/username**

Create a file `/etc/sudoers.d/username`.

```bash
sudo nano /etc/sudoers.d/username
```

Add the following line to grant `username` sudo privileges without a password.

```scss
username ALL=(ALL) NOPASSWD:ALL
```
