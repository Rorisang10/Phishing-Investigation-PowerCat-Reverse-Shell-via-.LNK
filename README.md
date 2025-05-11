# 📧 Phishing Investigation – PowerCat Reverse Shell

This project documents my hands-on investigation of a simulated phishing alert from TryHackMe. The scenario involved a malicious ZIP file disguised as an invoice, ultimately leading to the discovery of a PowerShell reverse shell payload using **PowerCat**.

---

## 🕵️‍♂️ Summary

- **Data Source**: Email
- **Recipient**: Michael Ascot (CEO)
- **Attachment**: `ImportantInvoice-Febrary.zip`
- **Host**: 3450
- **Malware Type**: Reverse Shell (PowerCat)
- **Tools Used**: PowerShell, VirusTotal, TryDetectThis, Splunk

---

## 🧪 Steps Taken

1. **Initial Triage**
   - Identified misspellings in the subject and attachment (`Invioce`, `Febrary`)
   - Flagged as suspicious due to social engineering and poor grammar  
   ![Phishing Email Screenshot](path/to/phis![Screenshot 2025-05-11 113143](https://github.com/user-attachments/assets/200e1cc3-986e-4c9f-8e02-e2fd1bdc6327)
hing-email.png)

2. **File Extraction & Analysis**
   - Extracted `.zip` archive: contained a disguised `.LNK` (shortcut) file
   - Used PowerShell's `more` function to read contents
   - Discovered embedded PowerShell script executing **PowerCat**  
   ![LNK File Contents](path/to/lnk-fi![Screenshot 2025-05-11 100749](https://github.com/user-attachments/assets/99b840c1-ba7a-45dc-bb6c-ba308f38db05)
le.png)

3. **Hash Reputation Check**
   - Generated file hashes using `TryDetectThis`
   - No results found on **VirusTotal**  
   ![Hash Analysis](path/to/hash-analy![Screenshot 2025-05-11 110500](https://github.com/user-attachments/assets/43762438-a1c9-4a34-9607-7902de69d9f7)
sis.png)

4. **Splunk Correlation**
   - Host `3450` (assigned to CEO) was searched via Splunk
   - Found matching PowerShell script activity in logs – confirmed execution  
   ![Splunk Logs](path/to/splunk-log![Screenshot 2025-05-11 105254](https://github.com/user-attachments/assets/54a775a2-cfc2-47d8-bbaf-9f17de508e0a)
s.png)

---

## 🔍 Key Findings

- **Threat Vector**: Phishing email with compressed shortcut file
- **Payload**: PowerCat reverse shell enabling remote access
- **Persistence Risk**: Bypasses some AV tools due to use of native PowerShell

---

## 📚 MITRE ATT&CK Mapping

| Technique ID | Technique                  |
|--------------|----------------------------|
| T1566.001    | Spearphishing Attachment   |
| T1204        | User Execution             |
| T1027        | Obfuscated Files or Info   |
| T1059.001    | PowerShell                 |
| T1095        | Non-Application Layer Protocol (reverse shell) |

---

## 🚧 Lessons Learned

- File extensions can be misleading – always inspect deeply
- PowerShell abuse is still common and effective
- Endpoint visibility (via Splunk) is critical for full detection
- Reverse shells can be hidden in seemingly simple attachments

---

## 🛡️ Skills Demonstrated

- Email threat analysis
- File hash generation and malware triage
- PowerShell script inspection
- Host-level investigation using Splunk
- Threat hunting and IOC identification

---
