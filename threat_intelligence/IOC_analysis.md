# Phishing IOC Analysis Report - Free Coffee Voucher Campaign

**Rule**: SOC282 - Phishing Alert - Deceptive Mail Detected  
**Incident Date:** May 13, 2024  09:22 AM  
**Threat Type:** Phishing (Attachment + Credential Harvesting)  
**Analyst:** Kabir Poudel 

---

## Executive Summary

A phishing email from `free@coffeeshoop.com` targeting `felix@letsdefend.io` with a "Free Coffee Voucher" lure, 
containing `free-coffee.zip` attachment was sent. ANY.RUN sandbox analysis revealed high-risk behavior (score 17/20), 
password protection, and C2 to `coffeeshoop.com`. VirusTotal and security vendors confirmed malicious nature. IOCs included hashes, IPs, domains for immediate response.

![Phishing Email with Redeem Button & ZIP Attachment](threat_intelligence/IOC_phishingEmail_images/email.png) 

## Incident Details

**Email Metadata:**
| Field | Value |
|-------|-------|
| From | `free@coffeeshoop.com` |
| To | `felix@letsdefend.io` |
| Subject | `Free Coffee Voucher` |
| Date | `May 13, 2024, 09:22 AM` |
| Action | `Allowed` (SOC Flagged) |

![Sender/Receiver Email Headers](threat_intelligence/IOC_phishingEmail_images/receiverANDsender.png)
![SOC Phishing Alert](threat_intelligence/IOC_phishingEmail_images/phishingAlert.png) 

## Indicators of Compromise (IOCs)

### 🗂️ File Hashes & Properties
- Filename: free-coffee.zip
- Size: 79 KB (6.3 KB extracted)
- Compression: DEFLATE (100%)
- Magic: ZIP archive data, at least v2.0
- SHA1: c895f4a970c612bc51e0fc272c3f08283a13d34f
- SHA256: 6f33ae4bf134c49faa14517a275c039ca1818b24fc2304649869e399ab2fb389
- Bundled: Coffee.exe (Win32 EXE)

| Hash Type | Value (truncated) | Severity |
|-----------|-------------------|----------|
| SHA1 | `c895f4a970c61...` | **High** |
| SHA256 | `6f33ae4bf134c49f...` | **High** |

![ZIP Properties & Full Hashes](threat_intelligence/IOC_phishingEmail_images/hash.png) 

### 🌐 Network Indicators

![Contacted IPs & Autonomous Systems](threat_intelligence/IOC_phishingEmail_images/IPaddress.png) 

### 🔍 Sandbox Analysis (ANY.RUN)
- Executed process: Coffee.exe
- 41 TCP connections observed
- 28 HTTP requests generated
- 17 DNS queries made
- Repeated outbound connections to 37.120.233.226:3451
- All traffic originated from the same process
- Non-standard port usage (3451)
- Pattern suggests suspicious external communication (possible C2 behavior)

![ANY.RUN Verdict & Threat Tags](threat_intelligence/IOC_phishingEmail_images/anyRunAnalysis.png) 

### 📊 VirusTotal Analysis
- 17 / 64 security vendors flagged the file as malicious
- Community score: -11
- File type: ZIP (password-protected)
- Contains: Windows PE file
- Size: 29.82 KB
- Last analyzed: 2 days ago
- Popular threat label: trojan.zynomm
- Threat category: Trojan
- Family label: Zynomm
- Password protection may have limited full static analysis
- Detected anti-debug / sandbox evasion behavior 

![VirusTotal Detection Results](threat_intelligence/IOC_phishingEmail_images/virustotalAnalysis.png)

**Traffic Patterns:**
- HTTPS beaconing to Cloudflare-hosted phishing domain
- Coffee.exe process making repeated connections
- No ransomware indicators; credential theft likely 

## Threat Hunting Playbook

**Email Parsing Checklist** :  
✅ When was it sent? (May 13, 2024)  
✅ Sender SMTP? (free@coffeeshoop.com)  
✅ Recipient address? (felix@letsdefend.io)  
✅ Content suspicious? (URGENT voucher)  
✅ Attachments present? (free-coffee.zip)  

![Phishing Analysis Playbook](threat_intelligence/IOC_phishingEmail_images/playbook.png) 

## MITRE ATT&CK Mapping

| Tactic | Technique | Implementation |
|--------|-----------|----------------|
| **Initial Access** | T1566.001 | Spearphishing Attachment |
| **Execution** | T1204.002 | Malicious File |
| **Discovery** | T1082 | System Information |
| **C2** | T1071.001 | Web Protocols |

## Risk Assessment & Impact

| Risk Factor | Score | Rationale |
|-------------|-------|-----------|
| **Likelihood** | High | Multiple security vendors flagged the file; repeated outbound TCP connections observed |
| **Impact** | High |Trojan-class malware with suspected C2 communication and potential data compromise
Detectability	Medium	Password-protected ZIP and anti-debug techniques limit static and sandbox analysis |
| **Detectability** | Medium | Password protection evades scanning |


## Response & Mitigation

### 🚨 **Immediate Actions** (0-2 hours)
- Block domain: coffeeshoop.com
- Block IPs: 204.79.197.203, 37.120.233.226
- Password reset for felix@letsdefend.io

---
### Lab
<a href='https://app.letsdefend.io/monitoring'>
LetsDefend - SOC282 - Phishing Alert - Deceptive Mail Detected </a>
