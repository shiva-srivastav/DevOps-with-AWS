# User and Permission Management in Linux

Managing users, groups, and permissions in Linux is essential for system security and access control. This guide explains all types of users, permission levels, the role of groups, and directory structures associated with users.

## 1. Types of Users in Linux

### a) Root User
- The **root** user is the superuser with unrestricted access to all system files and commands.
- Can modify system settings, manage users, install software, and change any file’s permissions.
- To switch to root user:
  ```sh
  sudo su
  ```

### b) Regular Users
- Regular users have limited access and can only modify files they own.
- Created using:
  ```sh
  sudo adduser username
  ```
- Home directories are stored in `/home/username/`.

### c) System Users
- Used for system processes and services (e.g., `www-data`, `mysql`).
- Usually, they do not have home directories and cannot log in interactively.
- Listed in `/etc/passwd`.

### d) Service Accounts
- Special-purpose accounts used for running applications like databases and web servers.
- These users typically don’t have passwords and are managed by system administrators.

## 2. User Management

### Creating a New User
```sh
sudo adduser username
```
- This creates a new user with a home directory `/home/username`.

### Assigning a Password
```sh
sudo passwd username
```
- Sets or updates the user’s password.

### Deleting a User
```sh
sudo deluser username
```
- Removes the user but keeps their home directory.

```sh
sudo deluser --remove-home username
```
- Deletes the home directory as well.

### Checking User Information
```sh
id username
```
- Displays user ID (UID), group ID (GID), and group memberships.

```sh
whoami
```
- Shows the current logged-in user.

## 3. Group Management
Groups in Linux are used to manage permissions for multiple users efficiently. Instead of assigning permissions to individual users, groups allow collective permission management. 

### Purpose of Groups
- **Primary Group**: Each user has a primary group that is created along with the user.
- **Secondary Groups**: Users can belong to multiple groups to gain additional permissions.
- **Administrative Groups**: Some groups, such as `sudo`, grant elevated permissions.
- **Project-Based Groups**: Useful for organizing access to files among team members.

### Creating a Group
```sh
sudo addgroup groupname
```

### Adding a User to a Group
```sh
sudo usermod -aG groupname username
```
- The `-aG` flag ensures the user is **added** to the group without being removed from existing groups.

### Viewing Group Membership
```sh
groups username
```
- Displays the groups a user belongs to.

### Removing a User from a Group
```sh
sudo deluser username groupname
```

### Deleting a Group
```sh
sudo delgroup groupname
```

### Viewing All Groups
```sh
cat /etc/group
```
- This lists all groups and their members.

## 4. File and Directory Permissions

Each file and directory has permissions assigned to three types of users:
1. **Owner** (User who created the file)
2. **Group** (Users belonging to the same group)
3. **Others** (All other users on the system)

### Viewing Permissions
```sh
ls -l filename
```
Example output:
```
-rwxr--r-- 1 user group 1234 Jan 01 12:34 filename
```

| Symbol | Meaning        |
|--------|---------------|
| `r`    | Read          |
| `w`    | Write         |
| `x`    | Execute       |
| `-`    | No permission |

### Changing File Permissions
```sh
chmod 755 filename
```
- `7` (rwx) for owner, `5` (r-x) for group, `5` (r-x) for others.

```sh
chmod u=rwx,g=rx,o=rx filename
```
- Alternative method using symbolic notation.

### Changing File Ownership
```sh
sudo chown newowner filename
```
- Change the owner of a file.

```sh
sudo chown newowner:newgroup filename
```
- Change both the owner and the group.

## 5. Special Permissions
### SUID (Set User ID)
- When set, the file runs as the file owner, not the executing user.
- Set using:
  ```sh
  chmod u+s filename
  ```

### SGID (Set Group ID)
- Files inherit the group of the directory.
- Set using:
  ```sh
  chmod g+s directory
  ```

### Sticky Bit
- Used for directories where only the file owner can delete files.
- Set using:
  ```sh
  chmod +t directory
  ```

## 6. User-Specific Directories
### `/home/username/`
- Default home directory for each user.

### `/etc/passwd`
- Stores user account details.

### `/etc/shadow`
- Stores encrypted user passwords.

### `/etc/group`
- Contains group information.

### `/var/mail/username`
- Stores user email data.

### `/tmp/` and `/var/tmp/`
- Temporary directories where users can store files temporarily.

## 7. Managing Sudo Privileges
### Granting a User Sudo Access
To add a user to the sudo group:
```sh
sudo usermod -aG sudo username
```
- This allows the user to execute commands as an administrator.

### Editing Sudoers File
To edit sudo privileges:
```sh
sudo visudo
```
- Add the following line to grant full sudo access:
  ```sh
  username ALL=(ALL) ALL
  ```

## Example
### Step 1: Create a New User
```sh
sudo adduser devuser
```
- This creates a new user `devuser` with a home directory `/home/devuser`.

### Step 2: Create a New Group
```sh
sudo addgroup developers
```
- This creates a new group named `developers`.

### Step 3: Add the User to the Group
```sh
sudo usermod -aG developers devuser
```
- This ensures `devuser` is added to the `developers` group without removing them from existing groups.

### Step 4: Verify Group Membership
```sh
groups devuser
```
- This will output the groups that `devuser` is a member of.

### Step 5: Create a Shared Directory
```sh
sudo mkdir /dev_team
```
- Creates a directory `/dev_team` for the development team.

### Step 6: Assign Group Ownership
```sh
sudo chown :developers /dev_team
```
- This sets the group `developers` as the owner of `/dev_team`.

### Step 7: Set Permissions for the Group
```sh
sudo chmod 770 /dev_team
```
- This gives full access (`rwx`) to the owner and group while restricting access to others.

### Step 8: Test Permissions
- Switch to `devuser`:
  ```sh
  su - devuser
  ```
- Try creating a file in `/dev_team`:
  ```sh
  touch /dev_team/testfile.txt
  ```
- If successful, the setup is working correctly.

## Conclusion
Understanding Linux users, groups, permissions, and directory structures is essential for effective system management. Groups simplify permission management and help enforce access control across multiple users efficiently. By mastering these commands and concepts, administrators can ensure secure and organized access control.


