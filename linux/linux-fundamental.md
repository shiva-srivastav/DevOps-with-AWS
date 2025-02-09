# Linux Fundamentals Detailed Guide

## File System Hierarchy Standard (FHS)

### Root Directory (/)
- The base of the Linux file system
- All other directories branch from here

### Key Directories
- **/bin**: Essential command binaries
  - Contains basic commands like `ls`, `cp`, `mv`
  - Available to all users
  - Required for system boot and repair

- **/boot**: Boot loader files
  - Kernel images
  - Initial RAM disk
  - Boot loader configuration (GRUB)

- **/dev**: Device files
  - Hardware devices
  - Pseudo-devices
  - Virtual devices

- **/etc**: System configuration
  - System-wide configuration files
  - Network configuration
  - User authentication files

- **/home**: User home directories
  - Personal files
  - User-specific configurations
  - Default location for downloads

- **/lib**: System libraries
  - Shared libraries needed by binaries
  - Kernel modules

- **/mnt, /media**: Mount points
  - Temporary file systems
  - Removable media

- **/opt**: Optional software
  - Third-party applications
  - Add-on packages

- **/proc**: Process information
  - Virtual filesystem
  - System information
  - Process details

- **/root**: Root user's home
  - Administrator's home directory
  - Restricted access

- **/sbin**: System binaries
  - System administration commands
  - Boot required binaries

- **/tmp**: Temporary files
  - Cleared on reboot
  - World-writable

- **/usr**: User programs
  - Applications
  - Libraries
  - Documentation

- **/var**: Variable data
  - Logs
  - Spool files
  - Temporary files that persist across reboots

## Basic Terminal Navigation

### Essential Navigation Commands
```bash
pwd     # Print Working Directory
cd      # Change Directory
ls      # List files and directories
```

### Directory Navigation Examples
```bash
cd /         # Go to root directory
cd ~         # Go to home directory
cd ..        # Go up one directory
cd -         # Go to previous directory
```

### Listing Files
```bash
ls           # Basic listing
ls -l        # Long format
ls -a        # Show hidden files
ls -lh       # Human-readable sizes
ls -R        # Recursive listing
```

## File and Directory Operations

### Creating Directories
```bash
mkdir directory_name
mkdir -p parent/child/grandchild    # Create parent directories if needed
```

### Copying Files and Directories
```bash
cp source destination
cp -r source_dir destination_dir    # Recursive copy
```

### Moving/Renaming Files
```bash
mv source destination
```

### Removing Files and Directories
```bash
rm file
rm -r directory    # Recursive removal
rm -f file        # Force removal
rmdir directory   # Remove empty directory
```

## Understanding Paths

### Absolute Paths
- Start from root directory (/)
- Complete path from root
- Example: `/home/user/documents/file.txt`

### Relative Paths
- Based on current directory
- Uses special notations:
  - `.` (current directory)
  - `..` (parent directory)
- Example: `../documents/file.txt`

## File Permissions and Ownership

### Permission Types
- Read (r): 4
- Write (w): 2
- Execute (x): 1

### Permission Categories
- User (u)
- Group (g)
- Others (o)

### Changing Permissions
```bash
chmod 755 file    # Using numeric mode
chmod u+x file    # Using symbolic mode
```

### Changing Ownership
```bash
chown user:group file
```

## Basic Text Editors

### Nano
- Beginner-friendly
- Menu-driven interface
- Basic commands:
  - `Ctrl + O`: Save
  - `Ctrl + X`: Exit
  - `Ctrl + W`: Search
  - `Ctrl + K`: Cut line

### Vim
- Advanced text editor
- Modal editing
- Basic modes:
  - Normal mode (Esc)
  - Insert mode (i)
  - Command mode (:)
- Essential commands:
  - `:w` - Save
  - `:q` - Quit
  - `:wq` - Save and quit
  - `:q!` - Force quit without saving

## Manual Pages and Help

### Using Man Pages
```bash
man command_name
man -k keyword    # Search man pages
```

### Help Commands
```bash
command --help    # Brief help
info command      # Detailed documentation
whatis command    # One-line description
```

### Navigation in Man Pages
- Space: Next page
- b: Previous page
- /pattern: Search forward
- ?pattern: Search backward
- q: Quit

### Tips for Learning
1. Practice basic commands daily
2. Use man pages regularly
3. Create test directories for practice
4. Start with nano before moving to vim
5. Understand permissions before modifying them
6. Keep a cheat sheet handy for reference