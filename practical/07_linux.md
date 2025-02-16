# Linux File Permissions and User Management - Practical Assignment

## Environment Setup
You are working as a DevOps engineer at TechCorp, managing a development server. The server details are:
- EC2 Instance running Amazon Linux 2
- IP Address: 13.235.67.89
- Initial access: Using key pair 'techcorp.pem'
- Base user: ec2-user

## Scenario
TechCorp is setting up a new project that requires:
- Two development teams: Frontend and Backend
- Shared resource directory for both teams
- Restricted access to configuration files
- Secure user management

## Assignment Tasks

### Task 1: User Management
Create the following structure:
- Frontend team members: alex, sarah
- Backend team members: mike, david
- Create groups: frontend-dev, backend-dev
- All developers should have sudo access

**Solution:**
```bash
# Create groups
$ sudo groupadd frontend-dev
$ sudo groupadd backend-dev

# Create users and add to groups
# Frontend team
$ sudo useradd -m -G frontend-dev,sudo alex
$ sudo useradd -m -G frontend-dev,sudo sarah

# Backend team
$ sudo useradd -m -G backend-dev,sudo mike
$ sudo useradd -m -G backend-dev,sudo david

# Set passwords
$ sudo passwd alex
$ sudo passwd sarah
$ sudo passwd mike
$ sudo passwd david

# Verify group memberships
$ groups alex
$ groups mike
```

### Task 2: Project Directory Structure
Create and configure the following directory structure:
```
/projects/
├── frontend/
├── backend/
└── shared/
    ├── assets/
    └── configs/
```

**Solution:**
```bash
# Create directory structure
$ sudo mkdir -p /projects/{frontend,backend,shared}/{assets,configs}

# Set group ownership
$ sudo chown -R root:frontend-dev /projects/frontend
$ sudo chown -R root:backend-dev /projects/backend
$ sudo chown -R root:root /projects/shared

# Set base permissions
$ sudo chmod 770 /projects/frontend
$ sudo chmod 770 /projects/backend
$ sudo chmod 775 /projects/shared
```

### Task 3: Permission Configuration
Configure specific permissions for different directories:
1. Frontend team: Full access to frontend/, read access to shared/
2. Backend team: Full access to backend/, read access to shared/
3. configs/ directory: Only readable by group owners

**Solution:**
```bash
# Configure frontend directory
$ sudo chmod -R 770 /projects/frontend
$ sudo setfacl -m g:backend-dev:r-x /projects/frontend

# Configure backend directory
$ sudo chmod -R 770 /projects/backend
$ sudo setfacl -m g:frontend-dev:r-x /projects/backend

# Configure shared directory
$ sudo chmod -R 775 /projects/shared
$ sudo chmod -R 750 /projects/shared/configs
```

### Task 4: File Operations
Create test files and verify permissions:

**Solution:**
```bash
# Create test files
$ sudo -u alex touch /projects/frontend/test.html
$ sudo -u mike touch /projects/backend/test.py
$ sudo touch /projects/shared/configs/app.config

# Verify permissions
$ ls -l /projects/frontend/test.html
-rw-r--r-- 1 alex frontend-dev 0 Feb 15 10:00 test.html

$ ls -l /projects/backend/test.py
-rw-r--r-- 1 mike backend-dev 0 Feb 15 10:00 test.py

$ ls -l /projects/shared/configs/app.config
-rw-r----- 1 root root 0 Feb 15 10:00 app.config
```

### Task 5: Verification and Testing
Test the setup with various scenarios:

**Solution:**
```bash
# Test frontend developer access
$ sudo -u alex touch /projects/frontend/test2.html  # Should succeed
$ sudo -u alex touch /projects/backend/test2.py     # Should fail
$ sudo -u alex cat /projects/shared/configs/app.config  # Should succeed

# Test backend developer access
$ sudo -u mike touch /projects/backend/test2.py     # Should succeed
$ sudo -u mike touch /projects/frontend/test2.html  # Should fail
$ sudo -u mike cat /projects/shared/configs/app.config  # Should succeed
```

## Questions for Practice

1. How would you give temporary access to a contractor to the frontend directory?
2. What commands would you use to find all files owned by user 'alex'?
3. How would you recursively change ownership of all files in the frontend directory?
4. What permission number would you use to set read-write for owner and group, but no access for others?
5. How would you copy the permission settings from one directory to another?

## Solutions to Practice Questions

1. Temporary contractor access:
```bash
$ sudo useradd -m contractor1
$ sudo usermod -aG frontend-dev contractor1
# After contract ends:
$ sudo usermod -G "" contractor1  # Remove from all groups
$ sudo userdel -r contractor1     # Delete user and home directory
```

2. Find files owned by alex:
```bash
$ sudo find /projects -user alex
```

3. Recursive ownership change:
```bash
$ sudo chown -R alex:frontend-dev /projects/frontend
```

4. Permission setting:
```bash
$ sudo chmod 660 filename
```

5. Copy permissions:
```bash
$ getfacl source_dir | setfacl --set-file=- destination_dir
```

## Success Criteria
- All users can access their respective directories
- Shared resources are accessible to all developers
- Configuration files have restricted access
- Group permissions are properly set
- No permission errors in daily operations