# Networking Basics for Security Analysts

## Why Networking Matters in Security
Understanding networking fundamentals is critical for security analysts. Network traffic analysis, threat detection, incident response, and vulnerability assessment all require solid knowledge of how networks operate. This file covers essential networking concepts I learned during my security training.

---

## OSI & TCP/IP Models (Security View)
The OSI model divides networking into 7 layers: Physical (cables/signals), Data Link (MAC addresses, switches), Network (IP routing), Transport (TCP/UDP), Session, Presentation, and Application (HTTP/DNS).​

TCP/IP simplifies this into 4 layers: Network Access (hardware), Internet (IP/ICMP/ARP), Transport (TCP/UDP), and Application, used in real-world internet operations.
​
Analysts use these to troubleshoot packet captures (PCAPs) by inspecting headers at each layer for malicious patterns.

Knowing **where** an attack happens matters.
```
+-----------------------------+
| Layer 7 - Application       |  ← Phishing, SQLi, XSS
+-----------------------------+
| Layer 6 - Presentation     |  ← Encryption / Encoding
+-----------------------------+
| Layer 5 - Session          |  ← Session hijacking
+-----------------------------+
| Layer 4 - Transport        |  ← Port scanning, DoS
+-----------------------------+
| Layer 3 - Network          |  ← IP spoofing
+-----------------------------+
| Layer 2 - Data Link        |  ← ARP poisoning
+-----------------------------+
| Layer 1 - Physical         |  ← Cable / hardware attacks
+-----------------------------+
```
---

## IP Addressing & Subnetting
### IPv4
- Format: 32-bit address (e.g., 192.168.1.1)
- Classes: A, B, C, D (multicast), E (experimental)
- Private Ranges
  - Class A: 10.0.0.0/8
  - Class B: 172.16.0.0/12
  - Class C: 192.168.0.0/16
### IPv6
- Format: 128-bit address (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334)
- Advantages: Larger address space, built-in IPsec, no NAT required
- Security: Different attack vectors than IPv4, requires updated security controls
### Subnetting
- Purpose: Divide networks into smaller segments
- CIDR Notation: 192.168.1.0/24 (subnet mask 255.255.255.0)
- Security Benefit: Network segmentation limits lateral movement

### Security Relevance (why learn IP addresses)
- Identifying suspicious IP addresses  
- Distinguishing internal vs external traffic  
- Investigating brute-force or scanning attempts  

---

## Common Network Protocols

| Protocol | Port | Purpose | Security Concern |
|--------|------|------------------|-------------|
| HTTP | 80 | Web Traffic | Unencrypted traffic, susceptible to interception |
| HTTPS | 443 | Secure web traffic | Certificate misuse |
| FTP | 21 | File transfer | Plaintext credentials |
| SSH | 22 |Secure remote access | Brute-force attacks |
| SMTP | 25 | Email transmission | Email spoofing, phishing, spam |
| DNS | 53 | Domain name resolution | DNS tunneling, Cache poisoning |
| SMB | 445 | file sharing | Lateral movement, ransomware |
| SQL| 1433/3306 | Database connection| SQL injection, unauthorized access |
---

Security analysts look for:
- Unexpected open ports
- Internet-exposed services
- Port scanning activity

---

## Network Devices
### Switches
- Function: Forward frames based on MAC addresses
- Security Features: Port security, DHCP snooping, 802.1X authentication
- Attacks: CAM table overflow, MAC flooding

### Routers
- Function: Route packets between networks using IP addresses
- Security Features: ACLs, packet filtering, NAT
- Attacks: Route poisoning, unauthorized access

### Firewalls
- Types: Packet filtering, stateful inspection, next-generation (NGFW)
- Function: Control traffic based on security rules
- Best Practices: Default deny, least privilege, regular rule audits
```
 Incoming Traffic
       |
       v
+------------------+
| Firewall Rules   |
+------------------+
| Allow 443        |
| Block 22 (Public)|
| Allow Internal   |
+------------------+
       |
       v
 Allowed / Blocked
```

### IDS/IPS
- IDS (Intrusion Detection System): Monitors and alerts on suspicious activity
- IPS (Intrusion Prevention System): Actively blocks threats
- Deployment: Network-based (NIDS/NIPS) or host-based (HIDS/HIPS)

## Network Traffic Analysis
### Packet Capture Tools
- Wireshark: GUI-based packet analyzer
- tcpdump: Command-line packet capture
- tshark: Command-line version of Wireshark

### Key Analysis Techniques
- Baseline normal traffic patterns
- Identify anomalies: unusual protocols, ports, traffic volumes
- Follow TCP streams to reconstruct sessions
- Examine packet headers and payloads
- Correlate with other security data (logs, alerts)

## Common Indicators of Compromise (IOCs)

- Unusual outbound connections
- Non-standard ports for common protocols
- Excessive DNS queries
- Large data transfers to external IPs
- Repeated failed login attempts
- Beaconing behavior (regular intervals)

## Network Security Architecture
### Defense in Depth
Implement multiple layers of security controls:
- Perimeter security (firewalls, IPS)
- Network segmentation (VLANs, DMZ)
- Access controls (NAC, 802.1X)
- Encryption (VPN, TLS)
- Monitoring and logging (SIEM, NetFlow)

### Network Segmentation
- Purpose: Isolate critical assets, limit lateral movement
- Methods: VLANs, physical separation, firewalls
- Common Segments: DMZ, production, development, guest networks

### Zero Trust Model
- Principle: Never trust, always verify
- Implementation: Micro-segmentation, continuous authentication, least privilege access

## Common Network Attacks
### Reconnaissance
- Port scanning (Nmap)
- Network mapping
- Banner grabbing
- OSINT gathering

### Man-in-the-Middle (MitM)
- ARP spoofing
- DNS spoofing
- SSL stripping
- Rogue access points

### Denial of Service (DoS/DDoS)

- SYN floods
- UDP floods
- ICMP floods
- Application-layer attacks (Slowloris)

### Lateral Movement

- Pass-the-hash
- Pass-the-ticket
- Remote service exploitation
- Internal phishing

## Network Monitoring Best Practices

- Enable comprehensive logging on all network devices
- Implement NetFlow or similar for traffic analysis
- Deploy IDS/IPS at strategic network points
- Monitor DNS queries for C2 communication and data exfiltration
- Establish baselines for normal network behavior
- Correlate network data with endpoint and application logs
- Use threat intelligence feeds to identify known malicious IPs/domains
- Regularly review firewall rules and ACLs
- Implement network access control (NAC)
- Conduct periodic network scans to identify vulnerabilities

## Tools for Security Analysts
### Traffic Analysis
- Wireshark, tcpdump, tshark
- NetworkMiner
- Zeek (formerly Bro)

### Network Scanning
- Nmap
- Masscan
- Angry IP Scanner

### Packet Crafting
- Scapy
- hping3

### Network Monitoring
- Nagios
- PRTG
- SolarWinds

### SIEM Integration
- Splunk
- ELK Stack (Elasticsearch, Logstash, Kibana)
- QRadar

## Key Takeaways
For security analysts, networking knowledge enables you to:
- Analyze network traffic for threats and anomalies
- Understand how attacks traverse networks
- Configure security controls effectively
- Investigate incidents using packet captures
- Design secure network architectures
- Communicate effectively with network teams
