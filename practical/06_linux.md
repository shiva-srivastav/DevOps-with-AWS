# Linux Command-Line Practice Guide

## Practice Environment Setup

### Initial Setup
```bash
# Create main practice directory
mkdir ~/linux_practice
cd ~/linux_practice

# Create scenario-specific directories
mkdir -p {config_files,logs,user_management,sudo_practice,backup,project_files}
```

### Scenario-Specific Environment Setup

#### 1. Text File Management Environment
```bash
cd ~/linux_practice/config_files

# Create sample configuration files
cat > server_config.txt << EOF
Server1 IP: 192.168.1.100 
Backup Server: 192.168.1.100
Database: mongodb://192.168.1.100:27017
Redis: 192.168.1.100:6379
Load Balancer: 192.168.1.100:80
EOF

# Create backup configuration
cat > app_config.txt << EOF
APP_SERVER=192.168.1.100
DB_SERVER=192.168.1.100
CACHE_SERVER=192.168.1.100
EOF
```

## Scenario 1: Text File Management
**Objective**: Update server IP addresses in configuration files

**Tasks & Solutions**:
1. Replace first occurrence in server_config.txt
```bash
# Preview changes
sed 's/192.168.1.100/192.168.1.200/' server_config.txt

# Make change with backup
sed -i.bak 's/192.168.1.100/192.168.1.200/' server_config.txt
```

2. Update all server entries in app_config.txt
```bash
# Replace all occurrences
sed -i.bak 's/192.168.1.100/192.168.1.200/g' app_config.txt
```

3. Verify changes
```bash
# Check both files
cat server_config.txt
cat app_config.txt
```

### 2. Project Files Environment Setup
```bash
cd ~/linux_practice/project_files

# Create sample project files
for i in {1..3}; do
    echo "Project $i Documentation" > project${i}.txt
    echo "Content for project $i" >> project${i}.txt
    echo "Status: In Progress" >> project${i}.txt
done

# Set appropriate permissions
chmod 644 project*.txt
```

## Scenario 2: Project Files Management
**Objective**: Manage project files and permissions

**Tasks & Solutions**:
1. List and sort projects
```bash
# List all projects
ls -l project*.txt

# Sort by modification time
ls -lt project*.txt
```

2. Add content to specific project
```bash
# Append to project1.txt
echo "Updated: $(date)" >> project1.txt
```

3. Change permissions
```bash
# Make all projects read-only
chmod 444 project*.txt
```

### 3. Log Files Environment Setup
```bash
cd ~/linux_practice/logs

# Create sample log file with mixed content
cat > app.log << EOF
[2024-02-09 10:00:01] INFO: Application started
[2024-02-09 10:00:02] DEBUG: Initializing database connection
[2024-02-09 10:00:03] ERROR: Failed to connect to backup server
[2024-02-09 10:00:04] DEBUG: Retrying connection...
[2024-02-09 10:00:05] INFO: Connected to primary server
[2024-02-09 10:00:06] DEBUG: Loading user preferences
[2024-02-09 10:00:07] WARNING: High memory usage detected
[2024-02-09 10:00:08] DEBUG: Garbage collection started
[2024-02-09 10:00:09] INFO: System stable
EOF

# Create rotated log files
cp app.log app.log.1
gzip app.log.1
```

## Scenario 3: Log Analysis
**Objective**: Analyze and manage log files

**Tasks & Solutions**:
1. Extract error messages
```bash
grep "ERROR" app.log
```

2. Remove DEBUG messages
```bash
# Remove with backup
sed -i.bak '/DEBUG/d' app.log
```

3. Count by log level
```bash
echo "Error Count: $(grep -c "ERROR" app.log)"
echo "Info Count: $(grep -c "INFO" app.log)"
echo "Warning Count: $(grep -c "WARNING" app.log)"
```

### 4. User Management Setup
```bash
cd ~/linux_practice/user_management

# Create test user directories
sudo mkdir -p /home/john/projects
cd /home/john/projects

# Create sample project files for John
sudo bash -c 'cat > project1.txt << EOF
Project Status: In Progress
Priority: High
Deadline: March 2024
Tasks:
- API Integration
- Database Migration
- Security Updates
EOF'

sudo bash -c 'cat > project2.txt << EOF
Client Requirements:
1. User Authentication
2. Payment Gateway
3. Reporting System
Status: 70% Complete
EOF'

sudo bash -c 'cat > important_notes.txt << EOF
Server Credentials:
- Dev Server: dev.example.com
- Test Environment: test.example.com
- Database Backups: Daily at 2 AM
EOF'

# Set ownership
sudo chown -R john:john /home/john/projects
```

## Scenario 4: User Management
**Objective**: Transfer user data and manage permissions

**Tasks & Solutions**:
1. Backup John's data
```bash
# Create backup
sudo tar -czf /backup/john_backup.tar.gz /home/john/projects/
```

2. Create new user and transfer files
```bash
# Create Sarah's account
sudo useradd -m sarah

# Copy with permissions
sudo cp -a /home/john/projects/. /home/sarah/projects/
sudo chown -R sarah:sarah /home/sarah/projects/
```

3. Verify transfer
```bash
# Check ownership and permissions
ls -la /home/sarah/projects/
```

### 5. Sudo Practice Environment Setup
```bash
cd ~/linux_practice/sudo_practice

# Create command list file
cat > allowed_commands.txt << EOF
Available Commands:
/sbin/ifconfig
/bin/netstat
/bin/ping
/usr/bin/docker
/usr/bin/kubectl
EOF

# Create test scripts for sudo practice
cat > network_test.sh << EOF
#!/bin/bash
ifconfig
netstat -tulpn
ping -c 4 localhost
EOF

chmod +x network_test.sh
```

## Scenario 5: Sudo Access Management
**Objective**: Configure and test sudo access

**Tasks & Solutions**:
1. Configure sudo access
```bash
# Open sudoers safely
sudo visudo

# Add line for devops user
devops ALL=(ALL) /sbin/ifconfig, /bin/netstat, /bin/ping
```

2. Test configuration
```bash
# Run test script
sudo ./network_test.sh

# Verify allowed commands
sudo -l -U devops
```

3. Check command execution
```bash
# Test each command
sudo ifconfig
sudo netstat -tulpn
sudo ping -c 4 localhost
```

## Verification Steps for All Scenarios
- [ ] File contents are correct
- [ ] Permissions are set properly
- [ ] Backups are created
- [ ] Users have correct access
- [ ] Commands execute successfully

## Common Pitfalls to Avoid
1. Not checking file contents after sed operations
2. Forgetting to create backups
3. Incorrect permission settings
4. Not verifying user access
5. Missing sudo configuration testing

## Cleanup Script
```bash
cat > cleanup.sh << EOF
#!/bin/bash
echo "Cleaning up practice environment..."

# Remove practice directories
rm -rf ~/linux_practice/config_files/*
rm -rf ~/linux_practice/project_files/*
rm -rf ~/linux_practice/logs/*
rm -rf ~/linux_practice/sudo_practice/*
rm -rf ~/linux_practice/backup/*

# Reset permissions
chmod -R 644 ~/linux_practice
find ~/linux_practice -type d -exec chmod 755 {} \;

echo "Cleanup complete!"
EOF

chmod +x cleanup.sh
```