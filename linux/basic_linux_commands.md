# Basic Linux Commands and File Structure for Vagrant Users

If you are using Linux within a Vagrant environment, it is essential to understand the basic Linux commands, file structure, and how to work with the `vi` editor. This guide will help you navigate Linux efficiently.

## 1. Linux File System Structure
Linux has a hierarchical directory structure. Below are some essential directories:

```
/		Root directory (base of the file system)
/bin		Essential binaries (ls, cp, mv, etc.)
/etc		Configuration files (system-wide settings and services)
/home		User home directories (each user gets a unique directory)
/var		Variable data (logs, databases, mail, temporary files)
/tmp		Temporary files (deleted after reboot)
/usr		User binaries and applications (non-essential system programs)
/dev		Device files (access to hardware components like disks and printers)
/mnt		Mounted drives (used to mount additional storage devices)
```
Understanding this structure helps in managing files efficiently.

## 2. Basic Linux Commands
### Navigation Commands
These commands help navigate through the Linux file system:
```sh
pwd         # Show current directory
ls          # List files and directories
ls -l       # List with details like permissions, owner, and size
ls -a       # Show hidden files
cd /path    # Change directory
cd ..       # Move up one level
```

### File and Directory Management
These commands help create, modify, and delete files and directories:
```sh
touch filename        # Create an empty file
mkdir dirname         # Create a new directory
rm filename           # Delete a file
rm -r dirname         # Delete a directory and its contents recursively
cp file1 file2        # Copy file1 to file2
mv file1 file2        # Move or rename file1 to file2
find /path -name file # Search for a file in the given path
```

### Viewing and Editing Files
Viewing file contents is crucial for troubleshooting and configuration:
```sh
cat filename          # Display file contents in one go
less filename         # View large files page by page (useful for logs)
tail -n 10 filename   # Show last 10 lines of a file (monitoring logs)
head -n 10 filename   # Show first 10 lines of a file (quick preview)
nano filename         # Edit file using nano editor (beginner-friendly)
vi filename           # Edit file using vi editor (powerful, requires learning curve)
```

## 3. Working with `vi` Editor
`vi` is a powerful text editor commonly used for Linux configuration files.

### Opening a File
```sh
vi filename
```

### Basic Modes in `vi`
- **Command Mode** (Default): Used for navigation and commands.
- **Insert Mode**: Press `i` to enter insert mode, allowing text entry.
- **Visual Mode**: Press `v` to select text for copying or deleting.

### Common `vi` Commands
| Command | Description |
|---------|-------------|
| `i` | Enter insert mode to start editing |
| `ESC` | Exit insert mode and return to command mode |
| `:w` | Save file without exiting |
| `:q` | Quit `vi` if no changes were made |
| `:q!` | Quit without saving changes |
| `:wq` | Save and quit `vi` |
| `dd` | Delete the current line |
| `yy` | Copy the current line |
| `p` | Paste the copied line after the cursor |
| `/word` | Search for "word" in the file |

Mastering `vi` improves efficiency when editing Linux configuration files.

## 4. User and Permission Management
Managing users and file permissions is essential for security and organization:
```sh
whoami                # Show current logged-in user
id                    # Show user ID and group ID
ls -l filename        # Show file permissions
chmod 755 filename    # Change permissions (owner, group, others)
chown user:group file # Change file ownership
sudo command          # Run a command as root (admin privileges)
adduser username      # Create a new user
passwd username       # Change a user’s password
```

### File Permission Levels
Permissions are displayed as `rwx` (read, write, execute):
```
Owner   Group   Others
rwx     r--     r--
```
- `r` (read) = View file contents
- `w` (write) = Modify file contents
- `x` (execute) = Run the file as a program

## 5. Process and System Monitoring
Monitoring system resources and managing processes are important for system health:
```sh
top          # Display running processes and resource usage
ps aux       # Show active processes with details
kill PID     # Kill a process using its process ID
uptime       # Show how long the system has been running
free -m      # Display memory usage in MB
```

These commands help diagnose system performance issues.

## Conclusion
By learning these essential Linux commands, file structures, and `vi` editor basics, you will be more comfortable working within a Vagrant Linux environment. These commands are fundamental for system administration, development, and debugging. Keep practicing and exploring for deeper understanding.

