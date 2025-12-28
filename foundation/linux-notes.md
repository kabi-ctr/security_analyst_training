# Linux Basics for Security Analysts

## Why Linux Matters in Security
Most servers, cloud workloads, containers, firewalls, SIEM collectors, and security tools run on Linux.  
A Security Analyst must be comfortable **navigating, monitoring, and investigating** Linux systems.

---

## 1. File System Structure (What to Watch)

```
├── bin → Essential binaries (ls, cp, cat)
├── sbin → System/admin binaries (iptables, ifconfig)
├── etc → Configuration files ⭐
├── var → Logs & variable data ⭐
├── log → System & application logs
├── home → User directories
├── tmp → Temporary files (often abused)
├── usr → User programs & libraries
└── root → Root user home
```

### Security Focus
- `/etc/passwd`, `/etc/shadow` → user & password data
- `/var/log/` → incident investigation
- `/tmp`, `/var/tmp` → malware often hides here

---

## 2. Users, Groups & Privileges

### Important Files
```bash
/etc/passwd   # User accounts
/etc/shadow   # Password hashes
/etc/group    # Groups
```
### Key Commands
```
whoami # Currently logged in users
id
groups
last
lastlog
```
### Privilege Escalation Awareness
`sudo -l  `      # Check allowed sudo commands

## 3. File Permissions & Ownership
### Permission Model
```
r = read (4)
w = write (2)
x = execute (1)
```
*Example:*
`-rwxr-x--- 1 root admin script.sh`

**Commands**
```
ls -l
chmod 750 file
chown root:admin file
```

## 4. Process & Service Monitoring
```
ps aux                     # All running processes
ps -ef                     # Alternative process listing
top                        # Real-time process monitoring
htop                       # Enhanced interactive process viewer
pstree                     # Process tree view
lsof                       # List open files and network connections
lsof -i                    # Show network connections only
lsof -p <PID>             # Files opened by specific process
```

## 5. Nerwork Analysis
```
netstat -tulpn            # Active network connections (deprecated but common)
ss -tulpn                 # Modern replacement for netstat
ip addr show              # Network interfaces and IPs
ip route                  # Routing table
arp -a                    # ARP cache
tcpdump -i eth0           # Packet capture on interface
tcpdump -i any port 80    # Capture HTTP traffic on all interfaces
nmap -sV <target>         # Network scanning (if installed)
```
## 6. Log Analysis

```
/var/log/auth.log         # Authentication logs (Debian/Ubuntu)
/var/log/secure           # Authentication logs (RHEL/CentOS)
/var/log/syslog          # System logs
/var/log/messages        # General messages
/var/log/apache2/        # Apache web server logs
/var/log/nginx/          # Nginx logs

# Log analysis commands
tail -f /var/log/auth.log              # Follow log in real-time
grep "Failed password" /var/log/auth.log    # Search for failed logins
journalctl -xe                         # Systemd logs (recent entries)
journalctl -u ssh.service              # Logs for specific service
journalctl --since "1 hour ago"        # Time-based filtering
```
## Key Security Concepts
- Least Privilege: Users and processes should have minimum permissions necessary.
- Defense in Depth: Multiple layers of security controls.
- Indicators of Compromise (IOCs): Signs of potential security incidents such as unusual processes, unexpected network connections, modified system files, or new user accounts.
- Chain of Custody: Document all actions taken during incident response for legal purposes.
- Volatile vs Non-Volatile Data: Memory contents disappear on reboot (volatile); disk data persists (non-volatile). Collect volatile data first during investigations.

### Common Attack Vectors to Monitor

- Brute force login attempts
- Privilege escalation via SUID binaries
- Backdoor accounts or SSH keys
- Suspicious cron jobs
- Unusual network connections
- Webshells in web directories
- Modified system binaries

### Best Practices

- Always document your investigation steps
- Create backups before making changes
- Use read-only mounts when analyzing compromised systems
- Verify file hashes against known good copies
- Check for hidden files (ls -la)
- Monitor for processes running from /tmp or /dev/shm
- Review sudo and SSH configurations regularly

## Recommended sites to study
 <a href="https://app.cybrary.it/browse/course/linux-fundamentals-for-security-practitioners">
  Linux Fundamentals for Security Practitioners
</a>
---
<a href="https://academy.tcm-sec.com/p/linux-fundamentals">
  Linux 100: Fundamentals
</a>
