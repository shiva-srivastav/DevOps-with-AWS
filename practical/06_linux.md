# Practical Linux Command-Line Scenarios

## Setting Up Practice Environment

### Initial Setup
```bash
# Create and enter practice directory
mkdir ~/linux_practice
cd ~/linux_practice

# Create all required directories
mkdir {config_files,project_files,logs,user_files,sudo_practice}
```

## Practice Scenarios

### Scenario 1: Text File Management

**Situation**: Managing server configuration files with IP address updates.

**Environment Setup**:
```bash
cd ~/linux_practice/config_files

# Create sample configuration file
cat > server_config.txt << EOF
Server1 IP: 192.168.1.100 
Backup Server: 192.168.1.100
Database: mongodb://192.168.1.100:27017
Redis: 192.168.1.100:6379
Load Balancer: 192.168.1.100:80
EOF
```

**Tasks**:
1. Replace first occurrence of IP in each line
2. Replace all occurrences and save changes

**Solution**:
```bash
# For first occurrence only
sed 's/192.168.1.100/192.168.1.200/' server_config.txt

# For all occurrences with save
sed -i.bak 's/192.168.1.100/192.168.1.200/g' server_config.txt
```

### Scenario 2: User Account Setup

**Situation**: Setting up development team accounts with group access.

**Environment Setup**:
```bash
cd ~/linux_practice/project_files

# Create project files
for i in {1..3}; do
    echo "Project $i content" > project${i}.txt
done
```

**Tasks**:
1. Create developers group
2. Create user accounts
3. Configure group access
4. Verify setup

**Solution**:
```bash
# Create group and users
sudo groupadd developers
sudo useradd -m alice
sudo useradd -m bob
sudo useradd -m charlie

# Add to developers group
for user in alice bob charlie; do
    sudo usermod -aG developers $user
done

# Verify membership
grep developers /etc/group
```

### Scenario 3: Log File Cleanup

**Situation**: Managing application logs with different severity levels.

**Environment Setup**:
```bash
cd ~/linux_practice/logs

# Create sample log file
cat > app.log << EOF
[2024-02-09 10:00:01] INFO: Application started
[2024-02-09 10:00:02] DEBUG: Initializing database connection
[2024-02-09 10:00:03] ERROR: Failed to connect to backup server
[2024-02-09 10:00:04] DEBUG: Retrying connection...
[2024-02-09 10:00:05] INFO: Connected to primary server
EOF
```

**Tasks**:
1. Preview DEBUG lines
2. Remove DEBUG lines
3. Verify changes

**Solution**:
```bash
# Preview DEBUG lines
sed -n '/DEBUG/p' app.log

# Delete DEBUG lines with backup
sed -i.bak '/DEBUG/d' app.log
```

### Scenario 4: User Transition Management

**Situation**: Transferring user data during employee transition.

**Environment Setup**:
```bash
cd ~/linux_practice/user_files

# Create John's project structure
sudo mkdir -p /home/john/projects
cd /home/john/projects

# Create project files
sudo bash -c 'cat > project1.txt << EOF
Project Status: In Progress
Priority: High
Tasks:
- API Integration
- Database Migration
EOF'

sudo bash -c 'cat > project2.txt << EOF
Client Requirements:
1. User Authentication
2. Payment Gateway
Status: 70% Complete
EOF'

# Set ownership
sudo chown -R john:john /home/john/projects
```

**Tasks**:
1. Backup user data
2. Transfer ownership
3. Verify setup

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

### Scenario 5: Sudo Access Configuration

**Situation**: Configuring limited sudo access for DevOps engineer.

**Environment Setup**:
```bash
cd ~/linux_practice/sudo_practice

# Create allowed commands list
cat > allowed_commands.txt << EOF
Available Commands:
/sbin/ifconfig
/bin/netstat
/bin/ping
EOF
```

**Tasks**:
1. Configure sudo access
2. Test configuration
3. Verify permissions

**Solution**:
```bash
# Configure sudo access
sudo visudo

# Add to sudoers (using visudo)
devops ALL=(ALL) /sbin/ifconfig, /bin/netstat, /bin/ping

# Verify configuration
sudo visudo -c
```

## Directory Structure
```
linux_practice/
├── config_files/
│   └── server_config.txt
├── project_files/
│   ├── project1.txt
│   ├── project2.txt
│   └── project3.txt
├── logs/
│   └── app.log
├── user_files/
│   └── projects/
│       ├── project1.txt
│       └── project2.txt
└── sudo_practice/
    └── allowed_commands.txt
```

## Practice Guidelines
1. Always work in the practice environment
2. Create backups before changes
3. Verify results after each command
4. Check permissions after file operations
5. Document all configuration changes

## Verification Checklist
For each scenario:
- [ ] Environment setup complete
- [ ] Commands executed successfully
- [ ] Results verified
- [ ] Permissions correct
- [ ] Backups created

## Common Pitfalls
1. Not creating backups
2. Incorrect file permissions
3. Missing user/group verifications
4. Incomplete file transfers
5. Improper sudo configurations