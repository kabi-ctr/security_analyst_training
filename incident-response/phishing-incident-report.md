# Phishing Incident Report – SOC146

### What is Phishing?
Phishing is a social engineering attack where attackers impersonate legitimate entities to trick victims into:

- Revealing sensitive information (credentials, financial data, personal information)
- Clicking malicious links
- Opening malicious attachments
- Transferring money or resources
- Installing malware

### Red Flags in Phishing Emails
Sender Indicators
- Spoofed Display Name - Display name doesn't match email address
- Similar Domains - micr0soft.com instead of microsoft.com
- Free Email Services - Gmail, Yahoo, Outlook for business communications
- Typosquatting - amaz0n.com, paypa1.com
- No Display Name - Just email address visible
- External Sender Warnings - Missing or bypassed

# Lab by LetsDefend
<a href="https://app.letsdefend.io/challenge/phishing-email">
  Phishing Challenge
</a>

## Overview
**Severity:** High  
**Date/Time of Alert:** June 13, 2021, 02:13 PM  
**Rule Name:** SOC146 - Phishing Mail Detected - Excel 4.0 Macros  
**Event ID:** 93  
**Alert Type:** Exchange  
**Incident Source:** Real phishing attack (LetsDefend simulated alert)

---

## 1. Summary

On June 13, 2021, a phishing email containing a malicious attachment was detected by the SOC146 rule within the LetsDefend platform. The alert was triggered because the email carried an Excel 4.0 macro-enabled attachment designed to execute external code upon user interaction.

---

## 2. Detection Details

**SMTP Server IP:** `24.213.228.54`  
**Sender:** `trenton@tritowncomputers.com`  
**Recipient:** `lars@letsdefend.io`  
**Subject:** `RE: Meeting Notes`  
**Device Action:** Allowed (email delivered to user inbox)

The initial alert indicated the presence of a potentially malicious email that contained a compressed file with a macro-enabled spreadsheet (Excel 4.0). 
---

## 3. Investigation

### 3.1 Email Parsing

- Located the email with subject **“RE: Meeting Notes”** and noted sender, recipient, and originating SMTP IP.  
- The body contained a ZIP attachment: `11f44531fb088d31307d87b01e8eabff.zip`.  
- No URLs were found directly in the email body itself.

### 3.2 Attachment Analysis

The ZIP archive was extracted. Inside was a file named `research-1646684671.xls`, which was flagged as malicious by multiple security vendors and sandbox engines on VirusTotal. 

Further dynamic analysis revealed that the spreadsheet contained an Excel 4.0 macro that, when executed, made network connections to externally hosted content, including a **Command and Control (C2) URL**:  

- `https://nws.visionconsulting.ro:443/N1G1KCXA/dot.html`  
(*C2 server identified from malware behavior analysis*) 
### 3.3 User Interaction & Execution

Log management showed that a host (IP `172.16.17.57`) made an outbound connection to the C2 domain identified in the malware behavior, indicating the attachment was *opened and executed* by the recipient.

---

## 4. Containment & Remediation

### Immediate Actions

1. **Removed the malicious email** from the user’s inbox to prevent further interaction.  
2. **Identified the infected host:**  
   - Hostname: `LarsPRD`  
   - Associated IP: `172.16.17.57`  
3. **Isolated the host** from the network to prevent lateral spread and further C2 communication. 

### Cleanup Steps

- Performed malware cleanup including:  
  - Deleted malicious files  
  - Ended malicious processes  
  - Restored affected applications (e.g., Excel and any dropped DLLs)  
- Reset user credentials if there was evidence of credential theft or misuse.

### Long-Term Measures

- Add identified malicious IOCs to detection tools (firewall, IPS, EDR, etc.).  
- Enhance email filtering policies to block similar attachments.  
- User awareness and phishing training to mitigate future incidents.

---

## 5. Indicators of Compromise (IOCs)

- **Sender Email:** `trenton@tritowncomputers.com`  
- **SMTP IP:** `24.213.228.54`  
- **Malicious Attachment:** `11f44531fb088d31307d87b01e8eabff.zip`  
- **Malicious File:** `research-1646684671.xls`  
- **C2 Domain:** `nws.visionconsulting.ro` 

---

## 6. Conclusion

This incident was assessed as a **true positive** phishing attack involving a malicious macro-enabled spreadsheet attachment. The phishing email successfully bypassed initial controls and was executed by a user, resulting in outbound C2 traffic. Incident response contained the host, removed artifacts, and updated defenses accordingly.

---

## 7. Lessons Learned

- Macro-enabled Office documents remain a significant phishing vector if not properly controlled.  
- Endpoint and mail defenses should be tuned to detect and block known malicious macro behavior.  
- Regular training and phishing simulations can reduce the chances of execution by users.

---

