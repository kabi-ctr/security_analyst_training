# MITRE ATT&CK Mapping

This document demonstrates my understanding of the **MITRE ATT&CK** framework and provides examples of mapping threats to specific tactics and techniques. As a security analyst, understanding ATT&CK is crucial for 
threat detection, incident response, and building effective defense strategies.

---
### What is MITRE ATT&CK?
MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) is a globally accessible knowledge base of 
adversary tactics and techniques based on real-world observations. It serves as a foundation for threat modeling 
and methodology development in the cybersecurity community.

## Framework structure

The framework is organized into several key components:
- Tactics: The "why" - the adversary's tactical objective or reason for performing an action
- Techniques: The "how" - the specific methods adversaries use to achieve tactical objectives
- Sub-techniques: More granular descriptions of techniques
- Procedures: The specific implementation used by threat actors

---

## How to Use This Mapping

1. Identify attacker actions from logs or alerts
2. Map actions to **Tactic (Why)** and **Technique (How)**
3. Reference technique IDs (e.g., `T1059.001`)
4. Record evidence and detection sources

---

## ATT&CK Tactics Covered

| Tactic | Description |
|------|------------|
| Initial Access | How the attacker gained entry |
| Execution | Running malicious code |
| Persistence | Maintaining access |
| Privilege Escalation | Gaining higher permissions |
| Defense Evasion | Avoiding detection |
| Credential Access | Stealing credentials |
| Discovery | Learning the environment |
| Lateral Movement | Moving through systems |
| Command and Control | Communicating with attacker |
| Exfiltration | Stealing data |
| Impact | Disrupting systems |

---

## Technique Mapping Table

| Tactic | Technique | Technique ID | Evidence Observed | Detection Source |
|------|-----------|-------------|------------------|------------------|
| Initial Access | Phishing Attachment | T1566.001 | Malicious Excel macro | Email Gateway |
| Execution | PowerShell | T1059.001 | Encoded command | PowerShell Logs |
| Persistence | Registry Run Keys | T1547.001 | Suspicious autorun key | Registry Auditing |
| Credential Access | LSASS Dump | T1003.001 | Memory access attempt | EDR |
| Command & Control | Web Protocols | T1071.001 | HTTPS beaconing | Proxy / Firewall |

---

## Example: Phishing Incident Mapping

**Incident Summary**:  
User opened a malicious Excel attachment which executed PowerShell and contacted C2 infrastructure.

| Attack Step | MITRE Mapping |
|------------|---------------|
| Malicious email | T1566.001 – Phishing |
| Macro execution | T1059.001 – PowerShell |
| Persistence added | T1547.001 – Run Keys |
| C2 traffic | T1071.001 – Web Protocols |

---

## Detection and Mitigation Strategies

### High-Priority Techniques to Monitor
Based on common attack patterns, the following techniques should be prioritized for detection:

- **T1078 – Valid Accounts**  
  Monitor authentication logs for anomalies

- **T1059 – Command and Scripting Interpreter**  
  Track execution of PowerShell, `cmd.exe`, and `bash`

- **T1566 – Phishing**  
  Enforce email security controls and continuous user training

- **T1027 – Obfuscated Files or Information**  
  Perform file analysis and sandboxing

- **T1486 – Data Encrypted for Impact**  
  Enable file system monitoring and maintain reliable backups

---

### Defense-in-Depth Approach

#### Prevent
- Implement email filtering and sandbox analysis  
- Enforce the principle of least privilege  
- Deploy application whitelisting  
- Enable multi-factor authentication (MFA)

#### Detect
- Deploy EDR/XDR solutions mapped to MITRE ATT&CK techniques  
- Implement SIEM with correlation rules based on attack patterns  
- Monitor for suspicious process execution chains  
- Analyze network traffic for command-and-control (C2) communications

#### Respond
- Develop playbooks aligned with MITRE ATT&CK tactics  
- Maintain up-to-date incident response procedures  
- Conduct regular tabletop exercises using ATT&CK scenarios  
- Enable automated containment for high-confidence detections

---

## References

- <a href="https://attack.mitre.org/">
  MITRE ATT&CK Enterprise Matrix </a>
- <a href="https://mitre-attack.github.io/attack-navigator/">
  ATT&CK Navigator
</a>

---
