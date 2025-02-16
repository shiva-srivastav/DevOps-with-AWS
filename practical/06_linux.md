# Linux Command-Line Practice Guide

## Initial Environment Setup
```bash
# Create main practice directory
mkdir -p ~/linux_practice
cd ~/linux_practice

# Create scenario directories
mkdir -p {config,logs,users,sudo,backup}
```

## Scenario 1: Configuration Management

### Environment Setup
```bash
cd ~/linux_practice/config

# Create production config
cat > prod_config.txt << EOF
# Production Environment
APP_SERVER=192.168.1.100
DB_SERVER=192.168.1.100
CACHE_SERVER=192.168.1.100
REDIS_URL=redis://192.168.1.100:6379
MONGO_URL=mongodb://192.168.1.100:27017
EOF

# Create development config
cat > dev_config.txt << EOF
# Development Environment
APP_SERVER=192.168.1.100
DB_SERVER=192.168.1.100
CACHE_SERVER=192.168.1.100
EOF
```

### Practice Tasks
1. Update all IPs in prod_config.txt to 192.168.1.200
2. Update only the APP_SERVER in dev_config.txt
3. Add comments while preserving existing ones

### Solutions
```bash
# Task 1: Update all IPs in prod_config.txt
sed -i.bak 's/192.168.1.100/192.168.1.200/g' prod_config.txt

# Task 2: Update specific entry in dev_config.txt
sed -i.bak 's/^APP_SERVER=192.168.1.100/APP_SERVER=192.168.1.200/' dev_config.txt

# Task 3: Add comments
sed -i.bak '/^#/!s/^/# Modified: $(date) \n/' prod_config.txt
```

## Scenario 2: Log Management

### Environment Setup
```bash
cd ~/linux_practice/logs

# Create application log with mixed content
cat > app.log << EOF
[2024-02-16 10:00:01] INFO: Application startup
[2024-02-16 10:00:02] DEBUG: Loading configurations
[2024-02-16 10:00:03] ERROR: Database connection failed
[2024-02-16 10:00:04] DEBUG: Retrying connection
[2024-02-16 10:00:05] INFO: Database connected
[2024-02-16 10:00:06] WARNING: High memory usage
[2024-02-16 10:00:07] DEBUG: Running garbage collection
[2024-02-16 10:00:08] INFO: Memory optimized
EOF

# Create backup log
cp app.log app.log.1
gzip app.log.1
```

### Practice Tasks
1. Extract and count error messages
2. Remove debug messages
3. Implement log rotation
4. Create summary report

### Solutions
```bash
# Task 1: Extract and count errors
grep "ERROR" app.log
grep -c "ERROR" app.log

# Task 2: Remove debug messages
sed -i.bak '/DEBUG/d' app.log

# Task 3: Log rotation
mv app.log app.log.2
gzip app.log.2

# Task 4: Create summary
echo "Log Summary" > summary.txt
echo "Errors: $(grep -c "ERROR" app.log.1)" >> summary.txt
echo "Warnings: $(grep -c "WARNING" app.log.1)" >> summary.txt
echo "Info: $(grep -c "INFO" app.log.1)" >> summary.txt
```

## Scenario 3: User Management

### Environment Setup
```bash
cd ~/linux_practice/users

# Create project structure
sudo mkdir -p /home/developer/projects
cd /home/developer/projects

# Create project files
sudo bash -c 'cat > project1.txt << EOF
Project: Authentication Service
Status: In Progress
Priority: High
Team: Security
Tasks:
- Implement OAuth2
- Add JWT support
- Setup user roles
EOF'

sudo bash -c 'cat > project2.txt << EOF
Project: Payment Gateway
Status: Planning
Priority: Medium
Team: Finance
Tasks:
- API design
- Security review
- Integration tests
EOF'

# Set ownership
sudo chown -R developer:developer /home/developer/projects
```

### Practice Tasks
1. Create new user and group
2. Transfer project ownership
3. Setup correct permissions
4. Verify access

### Solutions
```bash
# Task 1: Create user and group
sudo groupadd devteam
sudo useradd -m -G devteam newdev

# Task 2: Transfer ownership
sudo cp -a /home/developer/projects/. /home/newdev/projects/
sudo chown -R newdev:devteam /home/newdev/projects/

# Task 3: Set permissions
sudo chmod -R 750 /home/newdev/projects/

# Task 4: Verify
sudo -u newdev ls -la /home/newdev/projects/
```

## Scenario 4: Sudo Access Control

### Environment Setup
```bash
cd ~/linux_practice/sudo

# Create allowed commands list
cat > commands.txt << EOF
# Networking Commands
/sbin/ifconfig
/bin/netstat
/bin/ping

# Docker Commands
/usr/bin/docker ps
/usr/bin/docker images
/usr/bin/docker-compose up

# Kubernetes Commands
/usr/bin/kubectl get pods
/usr/bin/kubectl describe pod
/usr/bin/kubectl logs
EOF

# Create test script
cat > network_check.sh << EOF
#!/bin/bash
echo "Network Status Check"
ifconfig
netstat -tulpn
ping -c 4 localhost
EOF

chmod +x network_check.sh
```

### Practice Tasks
1. Configure sudo access for specific commands
2. Test restricted access
3. Audit sudo usage
4. Implement command logging

### Solutions
```bash
# Task 1: Configure sudo access
sudo visudo -f /etc/sudoers.d/devops
# Add:
# devops ALL=(ALL) /sbin/ifconfig, /bin/netstat, /bin/ping

# Task 2: Test access
sudo -l -U devops
./network_check.sh

# Task 3: Enable sudo logging
sudo bash -c 'echo "Defaults logfile=/var/log/sudo.log" >> /etc/sudoers.d/logging'

# Task 4: Review logs
sudo tail -f /var/log/sudo.log
```

## Environment Cleanup
```bash
cat > ~/linux_practice/cleanup.sh << EOF
#!/bin/bash
echo "Cleaning practice environment..."

# Remove all created files
rm -rf ~/linux_practice/config/*
rm -rf ~/linux_practice/logs/*
rm -rf ~/linux_practice/users/*
rm -rf ~/linux_practice/sudo/*
rm -rf ~/linux_practice/backup/*

# Reset permissions
find ~/linux_practice -type d -exec chmod 755 {} \;
find ~/linux_practice -type f -exec chmod 644 {} \;

echo "Environment cleaned!"
EOF

chmod +x ~/linux_practice/cleanup.sh
```

## Best Practices
1. Always backup before making changes
2. Use version control for configurations
3. Test commands in safe environment
4. Document all system changes
5. Verify permissions after modifications
6. Keep audit logs of administrative actions

## Common Pitfalls
1. Forgetting to backup
2. Not testing in isolation
3. Incorrect permission settings
4. Incomplete cleanup
5. Insufficient logging
6. Overly permissive access

## Directory Structure
```
linux_practice/
├── config/
│   ├── prod_config.txt
│   └── dev_config.txt
├── logs/
│   ├── app.log
│   ├── app.log.1.gz
│   └── summary.txt
├── users/
│   └── projects/
│       ├── project1.txt
│       └── project2.txt
├── sudo/
│   ├── commands.txt
│   └── network_check.sh
├── backup/
└── cleanup.sh
```