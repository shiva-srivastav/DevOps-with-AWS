# Linux Command-Line Practice Scenarios

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

#### 2. Project Files Setup
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

#### 3. Log Files Environment
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

#### 4. User Management Setup
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

#### 5. Sudo Practice Environment
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

### Directory Structure Verification
```bash
tree ~/linux_practice
```

Expected structure:
```
linux_practice/
├── config_files/
│   ├── server_config.txt
│   └── app_config.txt
├── project_files/
│   ├── project1.txt
│   ├── project2.txt
│   └── project3.txt
├── logs/
│   ├── app.log
│   └── app.log.1.gz
├── user_management/
│   └── john/
│       ├── project1.txt
│       ├── project2.txt
│       └── important_notes.txt
├── sudo_practice/
│   ├── allowed_commands.txt
│   └── network_test.sh
└── backup/
```

### Environment Cleanup Script
```bash
cat > cleanup.sh << EOF
#!/bin/bash
# Cleanup script for practice environment

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

## Scenario 1: Text File Management
**Objective**: Update server IP addresses in configuration files

**Setup**:
```bash
cd ~/linux_practice/config_files
cat > config.txt << EOF
Server1 IP: 192.168.1.100 
Backup Server: 192.168.1.100
Database: mongodb://192.168.1.100:27017
Redis: 192.168.1.100:6379
EOF
```

**Tasks**:
1. Replace first occurrence of IP in each line
2. Replace all occurrences globally
3. Create backup before changes

**Solutions**:
```bash
# Preview changes (safe practice)
sed 's/192.168.1.100/192.168.1.200/' config.txt

# Replace first occurrence in each line with backup
sed -i.bak 's/192.168.1.100/192.168.1.200/' config.txt

# Replace all occurrences globally with backup
sed -i.bak 's/192.168.1.100/192.168.1.200/g' config.txt
```

## Scenario 2: User and Group Management
**Objective**: Set up development team accounts with proper group permissions

**Tasks**:
1. Create development group
2. Create user accounts
3. Configure group permissions
4. Verify setup

**Solution**:
```bash
# Create group
sudo groupadd developers

# Create users and add to group simultaneously
for user in alice bob charlie; do
    sudo useradd -m -G developers $user
    sudo passwd $user  # Set password
done

# Verify setup
getent group developers
id alice  # Check user's groups
```

## Scenario 3: Log Analysis and Management
**Objective**: Manage application logs with different severity levels

**Setup**:
```bash
cd ~/linux_practice/logs
cat > app.log << EOF
[2024-02-09 10:00:01] INFO: Application started
[2024-02-09 10:00:02] DEBUG: Initializing database
[2024-02-09 10:00:03] ERROR: Connection failed
[2024-02-09 10:00:04] DEBUG: Retrying connection
[2024-02-09 10:00:05] INFO: Connected successfully
EOF
```

**Tasks**:
1. Extract ERROR messages
2. Remove DEBUG messages
3. Count occurrences of each log level
4. Rotate logs

**Solutions**:
```bash
# Extract ERROR messages
grep "ERROR" app.log

# Remove DEBUG messages with backup
sed -i.bak '/DEBUG/d' app.log

# Count log levels
grep -c "INFO" app.log
grep -c "ERROR" app.log

# Log rotation (manual example)
mv app.log app.log.1
gzip app.log.1
```

## Scenario 4: User Transition Management
**Objective**: Transfer user data while maintaining security

**Setup**:
```bash
cd ~/linux_practice/user_management

# Create project structure
sudo mkdir -p /home/john/projects
sudo bash -c 'cat > /home/john/projects/project1.txt << EOF
Project: API Integration
Status: In Progress
EOF'
```

**Tasks**:
1. Backup user data
2. Transfer ownership
3. Preserve permissions
4. Verify integrity

**Solution**:
```bash
# Backup
sudo tar -czf /backup/john_backup.tar.gz /home/john/projects/

# Create new user and transfer
sudo useradd -m sarah
sudo cp -a /home/john/projects/. /home/sarah/projects/
sudo chown -R sarah:sarah /home/sarah/projects

# Verify
sudo -u sarah ls -la /home/sarah/projects/
```

## Scenario 5: Sudo Access Management
**Objective**: Configure granular sudo permissions for DevOps team

**Tasks**:
1. Create custom sudo rules
2. Allow specific commands
3. Maintain security

**Solution**:
```bash
# Open sudoers safely
sudo visudo

# Add specific permissions (add to file)
devops ALL=(ALL) /sbin/ifconfig, /bin/netstat, /bin/ping

# Test configuration
sudo visudo -c
```

## Best Practices
1. Always create backups before major changes
2. Use `-i.bak` with sed for automatic backups
3. Test commands with non-destructive options first
4. Verify permissions after changes
5. Document all system modifications
6. Use version control for configuration files

## Verification Steps
For each scenario:
- [ ] Test functionality
- [ ] Check permissions
- [ ] Verify backups
- [ ] Document changes
- [ ] Review security implications

## Additional Tips
1. Use `man` pages for detailed command information
2. Create test environments for practice
3. Keep logs of all major system changes
4. Implement regular backup schedules
5. Use configuration management tools for larger deployments

## Common Pitfalls to Avoid
1. Forgetting to backup before changes
2. Not testing commands in safe environment
3. Incorrect permission settings
4. Incomplete user transition procedures
5. Overly permissive sudo rights