# Incident Response Playbook

## Overview

This playbook provides standardized procedures for identifying, responding to, and recovering from security incidents. It follows the NIST Incident Response Lifecycle and is designed to minimize damage, reduce recovery time, and improve future security posture.

## Table of Contents

1. [Incident Response Team](#incident-response-team)
2. [Incident Classification](#incident-classification)
3. [Response Phases](#response-phases)
4. [Incident Types & Procedures](#incident-types--procedures)
5. [Tools & Resources](#tools--resources)

---

## Incident Response Team

### Core Team Members

| Role | Responsibilities |
|------|-----------------|
| **Incident Commander** | Overall response coordination, decision-making | 
| **Security Analyst** | Investigation, analysis, containment |
| **IT Operations** | System access, backups, infrastructure changes | 
| **Communications Lead** | Internal/external communications, stakeholder updates | 
| **Legal Counsel** | Legal implications, regulatory compliance | 

### Escalation Path

```
Security Analyst → Incident Commander → CISO → Executive Leadership
```

---

## Incident Classification

### Severity Levels

**Critical (P1)**: Immediate threat to business operations, data breach, ransomware
- Response Time: Immediate
- Escalation: Automatic to executive level

**High (P2)**: Significant security compromise, unauthorized access to sensitive systems
- Response Time: Within 1 hour
- Escalation: CISO notification required

**Medium (P3)**: Confirmed security incident with limited impact
- Response Time: Within 4 hours
- Escalation: Security team lead

**Low (P4)**: Suspicious activity requiring investigation
- Response Time: Within 24 hours
- Escalation: Standard security team

---

## Response Phases

### Phase 1: Preparation

**Objective**: Ensure readiness to handle security incidents effectively.

**Actions**:
- Maintain up-to-date contact lists for IR team
- Keep incident response tools accessible and tested
- Conduct quarterly tabletop exercises
- Review and update playbooks every 6 months
- Ensure backup systems are functional and tested

**Deliverables**:
- Current IR team roster
- Documented communication channels
- Verified tool access credentials

---

### Phase 2: Detection & Analysis

**Objective**: Identify and validate security incidents quickly and accurately.

**Initial Detection Sources**:
- Security Information and Event Management (SIEM) alerts
- Intrusion Detection System (IDS) alerts
- Antivirus/EDR alerts
- User reports
- Threat intelligence feeds

**Analysis Steps**:

1. **Triage** (0-15 minutes)
   - Verify the alert is legitimate
   - Determine affected systems/users
   - Assign initial severity rating
   - Document initial observations in incident ticket

2. **Investigation** (15 minutes - 2 hours)
   - Collect relevant logs (firewall, proxy, system, application)
   - Identify indicators of compromise (IOCs)
   - Determine attack vector and timeline
   - Assess scope and potential impact
   - Update severity classification if needed

3. **Documentation**
   - Create incident ticket with unique ID
   - Log all actions taken with timestamps
   - Capture screenshots and evidence
   - Maintain chain of custody for forensic data

**Key Questions to Answer**:
- What happened?
- When did it happen?
- How was it discovered?
- What systems/data are affected?
- Is the threat still active?
- What is the potential business impact?

---

### Phase 3: Containment

**Objective**: Limit the scope and impact of the incident.

#### Short-term Containment

**Immediate Actions** (varies by incident type):
- Isolate affected systems from network
- Disable compromised user accounts
- Block malicious IP addresses/domains at firewall
- Preserve evidence before making changes

**Decision Criteria**:
- Will containment alert the attacker?
- What is the risk of data loss?
- What is the business impact of containment actions?

#### Long-term Containment

**Actions**:
- Apply temporary security patches
- Implement additional monitoring on affected systems
- Deploy honeypots or deception technology
- Harden systems while maintaining business operations

---

### Phase 4: Eradication

**Objective**: Remove the threat from the environment completely.

**Actions**:
1. **Identify Root Cause**
   - Determine how the attacker gained access
   - Identify all compromised systems and accounts
   - Find and remove malware, backdoors, or persistence mechanisms

2. **Remove Threat Components**
   - Delete malicious files and scripts
   - Remove unauthorized user accounts or access
   - Close exploited vulnerabilities
   - Reset compromised credentials

3. **Verification**
   - Scan systems with multiple security tools
   - Review logs for signs of remaining compromise
   - Confirm IOCs are no longer present

---

### Phase 5: Recovery

**Objective**: Restore systems to normal operations safely.

**Recovery Steps**:

1. **Prepare for Recovery**
   - Verify systems are clean
   - Apply all security patches
   - Change all relevant passwords
   - Update security controls

2. **Restore Operations**
   - Restore from clean backups if necessary
   - Rebuild compromised systems from known-good sources
   - Gradually reconnect systems to network
   - Implement enhanced monitoring

3. **Validation**
   - Monitor systems closely for 48-72 hours
   - Verify business operations are normal
   - Confirm no signs of re-infection

**Recovery Priorities**:
1. Critical business systems
2. User-facing services
3. Internal systems
4. Development/test environments

---

### Phase 6: Lessons Learned

**Objective**: Improve incident response capabilities and prevent recurrence.

**Post-Incident Review** (within 2 weeks):

**Meeting Agenda**:
- What happened? (timeline of events)
- What worked well?
- What could be improved?
- What actions will we take?

**Documentation**:
- Detailed incident report
- Timeline with all actions taken
- Impact assessment
- Recommendations for improvement

**Follow-up Actions**:
- Implement security improvements
- Update playbooks and procedures
- Conduct training if gaps identified
- Share lessons with relevant teams

---

## Incident Types & Procedures

### 1. Malware Infection

**Indicators**:
- Antivirus/EDR alerts
- Unusual network traffic
- System performance degradation
- Unexpected file modifications

**Response Procedure**:
1. Isolate infected system from network immediately
2. Capture memory dump and disk image for analysis
3. Identify malware type and capabilities
4. Check for lateral movement to other systems
5. Remove malware using appropriate tools
6. Reimage system if rootkit suspected
7. Update antivirus signatures
8. Investigate infection vector

---

### 2. Phishing Attack

**Indicators**:
- User reports suspicious email
- Credential harvesting site detected
- Unusual login attempts after email campaign
- Email from spoofed sender

**Response Procedure**:
1. Analyze email headers and content
2. Identify all recipients
3. Block sender domain/IP at email gateway
4. Search and delete unread copies from mailboxes
5. If credentials entered: immediately reset affected accounts
6. Check logs for unauthorized access using compromised credentials
7. Notify affected users
8. Conduct security awareness training

---

### 3. Data Breach / Exfiltration

**Indicators**:
- Large outbound data transfers
- Database queries for sensitive information
- Access to data outside normal patterns
- Discovery of data on external sites

**Response Procedure**:
1. Identify compromised data and systems
2. Stop ongoing exfiltration immediately
3. Preserve evidence (logs, network captures)
4. Determine how data was accessed
5. Assess regulatory notification requirements (GDPR, HIPAA, etc.)
6. Notify legal counsel immediately
7. Prepare customer/public communications if required
8. Implement Data Loss Prevention (DLP) improvements

**Critical**: Legal counsel must be involved before external notification.

---

### 4. Ransomware

**Indicators**:
- Files encrypted with unusual extensions
- Ransom note on systems
- Inability to access files or systems
- Mass file modifications

**Response Procedure**:
1. **DO NOT pay ransom without executive approval and legal consultation**
2. Immediately isolate affected systems
3. Identify ransomware variant
4. Check for available decryption tools
5. Assess backup availability and integrity
6. Disable network shares and backups to prevent spread
7. Report to law enforcement (FBI, local authorities)
8. Restore from backups after confirming systems are clean
9. Implement email attachment filtering improvements

---

### 5. Insider Threat

**Indicators**:
- Unusual access patterns by authorized user
- Data accessed outside job responsibilities
- Large file downloads before termination
- Attempts to cover tracks

**Response Procedure**:
1. Discreetly gather evidence without alerting subject
2. Involve HR and Legal immediately
3. Document all suspicious activities with timestamps
4. Preserve logs and access records
5. Monitor user activity without alerting them
6. Plan coordinated account disablement if termination planned
7. Conduct exit interview and asset recovery
8. Review access controls and segregation of duties

**Special Considerations**: Privacy laws, employment law, and potential legal proceedings.

---

### 6. Denial of Service (DoS/DDoS)

**Indicators**:
- Service unavailability
- Extreme network traffic volume
- Server resource exhaustion
- Legitimate users cannot access services

**Response Procedure**:
1. Confirm it's a DDoS and not infrastructure failure
2. Activate DDoS mitigation service (Cloudflare, AWS Shield, etc.)
3. Block attacking IP ranges at firewall/ISP level
4. Enable rate limiting and traffic filtering
5. Scale resources if possible (cloud auto-scaling)
6. Communicate service status to users
7. Work with ISP for upstream filtering
8. Document attack characteristics for future defense

---

### 7. Unauthorized Access

**Indicators**:
- Login from unusual location/time
- Failed login attempts followed by success
- Privilege escalation attempts
- Access to unauthorized resources

**Response Procedure**:
1. Disable compromised account immediately
2. Review all actions taken by account
3. Check for creation of backdoor accounts
4. Identify access method (stolen creds, vulnerability, etc.)
5. Force password reset for affected users
6. Enable MFA if not already in place
7. Review and strengthen access controls
8. Check for data accessed or modified

---


## Tools & Resources

### Essential Tools

**Detection & Analysis**:
- SIEM platform
- Endpoint Detection and Response (EDR)
- Network traffic analyzer (Wireshark, tcpdump)
- Log analysis tools
- Threat intelligence platforms

**Containment & Eradication**:
- Firewall management console
- Active Directory/IAM tools
- Antivirus/anti-malware tools
- Forensic imaging tools

**Documentation**:
- Incident ticketing system
- Secure note-taking platform
- Screen capture tools
- Timeline creation tools

### External Resources

- **US-CERT**: https://www.cisa.gov/uscert
- **SANS Incident Response**: https://www.sans.org/incident-response
- **NIST Cybersecurity Framework**: https://www.nist.gov/cyberframework
- **Cybersecurity & Infrastructure Security Agency**: https://www.cisa.gov

