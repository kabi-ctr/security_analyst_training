# SOC Analyst Fundamentals

## What is a SOC?
A Security Operations Center (SOC) is a centralized unit that deals with security issues on an organizational and technical level. The SOC team monitors, detects, investigates, and responds to cybersecurity threats 24/7.

### SOC Functions
- Continuous Monitoring - Real-time surveillance of networks, systems, and applications
- Threat Detection - Identifying potential security incidents
- Incident Response - Responding to and mitigating security breaches
- Threat Intelligence - Gathering and analyzing information about threats
- Security Tool Management - Maintaining and tuning security technologies
- Compliance and Reporting - Ensuring adherence to security policies and regulations

### What Does a SOC Analyst Do?
A typical day involves:
- Monitoring security dashboards and SIEM platforms
- Triaging and prioritizing security alerts
- Investigating potential security incidents
- Performing log analysis and correlation
- Identifying false positives vs. real threats
- Escalating critical incidents to senior analysts
- Documenting findings and creating incident reports
- Tuning detection rules to reduce noise
- Collaborating with other IT teams


### SOC Analyst Tiers
- **Tier 1**: Monitor alerts, triage, escalate
- **Tier 2**: Deep investigation, containment
- **Tier 3**: Threat hunting, detection engineering

---


## Key SOC Tools
- **SIEM**: Splunk, Sentinel, QRadar
- **EDR/XDR**: CrowdStrike, Defender, SentinelOne
- **SOAR**: Automated response workflows
- **IDS/IPS**: Network-based detection
- **Threat Intelligence**: IOC feeds, MITRE ATT&CK

---
# Modern SOC Architecture: Log Pipeline & Data Flow
```
+-------------------------------------------------------------------+
| 1. COLLECTION LAYER (The Spokes)                                   |
|                                                                    |
|  [Endpoints]        [Network Devices]        [Cloud Services]      |
|  (EDR / Sysmon)     (Firewall / IPS)         (AWS / Azure Logs)    |
|       |                    |                        |              |
+-------+--------------------+------------------------+------------+
                                |
                                v
+-------------------------------------------------------------------+
| 2. PROCESSING LAYER (SIEM)                                         |
|                                                                    |
|      Encrypted Logs / Syslog                                       |
|              |                                                     |
|              v                                                     |
|      +------------------------+                                    |
|      |      SIEM Platform     |                                    |
|      |  (Splunk / Sentinel)   |                                    |
|      +------------------------+                                    |
|          |            |                                            |
|          |            +--> Parsing & Normalization Engine          |
|          |                         |                               |
|          |                         v                               |
|          |                   Correlation Engine                    |
|          |                         |                               |
|          +------------------------>+                               |
|                                    v                               |
|                             High-Fidelity Alerts                   |
+-------------------------------------------------------------------+
                                |
                                v
+-------------------------------------------------------------------+
| 3. ACTION LAYER (SOAR + Human)                                     |
|                                                                    |
|  +----------------------+        +------------------------------+  |
|  |   SOAR Platform      | -----> |     Security Analyst         |  |
|  |  (Playbooks)         |        |  (Investigation / Response)  |  |
|  |                      |        |                              |  |
|  |  - Alert Enrichment  |        |  - Triage & Prioritization   |  |
|  |    (VT / Threat Intel)|       |  - Incident Response         |  |
|  |  - Containment       |        |                              |  |
|  |    (Host Isolation)  |        +------------------------------+  |
|  +----------------------+                                          |
+-------------------------------------------------------------------+

```
## Incident Response Lifecycle

Detection → Analysis → Containment → Eradication → Recovery → Lessons Learned

1. Alert triggered by SIEM/EDR
2. Analyst investigates logs & behavior
3. Threat contained (isolation, blocking)
4. Root cause removed
5. Systems restored
6. Detection rules improved

---

## Common SOC Alert Types
- Phishing attempts
- Brute-force login attacks
- Malware execution
- Suspicious PowerShell activity
- Data exfiltration attempts

---

## KPIs Used in a SOC
- **MTTD** (Mean Time to Detect)
- **MTTR** (Mean Time to Respond)
- False positive rate
- Incident volume by severity

---

## Challenges Faced by SOC Teams
- Alert fatigue
- False positives
- Tool overload
- Skill gaps
- Evolving attacker techniques

---

## SOC vs NOC (Quick Comparison)

| SOC | NOC |
|----|----|
| Security-focused | Availability-focused |
| Handles threats | Handles outages |
| Uses SIEM/EDR | Uses monitoring tools |

---

## Why SOC Matters
A well-functioning SOC is critical for:
- Limiting breach impact
- Regulatory compliance
- Business continuity
- Improving organizational cyber resilience

---

## References
- MITRE ATT&CK Framework
- NIST Incident Response Lifecycle
