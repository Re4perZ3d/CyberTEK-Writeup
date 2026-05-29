# Operation GhostVein — Challenge Questions

> Original challenge questions, flag formats, and final flags for the **CyberTEK / Operation GhostVein** DFIR forensic scenario.

## 🎮 Play the Challenge

The original DFIR evidence package is still available for anyone who wants to try the scenario before reading the writeup:

📦 **Download evidence:**  
https://drive.google.com/file/d/1qJgTznQsHkGdYdmBSUG38QxmaHtQadZ2/view?usp=sharing

> ⚠️ **Recommendation:** Try solving the challenge first before reading the writeup, as the writeup contains full spoilers and flags.

---

## 1. Yoo — Evidence Integrity

**Question:**  
Welcome to Operation GhostVein.

Download the DFIR evidence handout:  
https://drive.google.com/file/d/1qJgTznQsHkGdYdmBSUG38QxmaHtQadZ2/view?usp=sharing

Your first task is to verify the integrity of the archive and submit its SHA256 hash.

**Flag format:** `CyberTEK{sha256sum}`

**Flag:**  
```text
CyberTEK{624ca5deb58c36080924c1e5bae7cbe3431d4cae5d6883700bf9081ef791737f}
```

---

## 2. Zyyz 1 — Initial Access CVE

**Question:**  
The first signs of compromise point toward the public-facing ERP/OFBiz server.

Identify the CVE that was exploited for initial access against the OFBiz server.

**Flag format:** `CyberTEK{CVE-YYYY-NNNNN}`

**Flag:**  
```text
CyberTEK{CVE-2024-38856}
```

---

## 3. Zyyz 2 — First Contact Timestamp

**Question:**  
The attacker touched the OFBiz server before the full compromise chain began.

Determine the timestamp of the attacker's first request to the OFBiz server.

**Flag format:** `CyberTEK{DD_Mon_YYYY:HH:MM:SS}`

**Flag:**  
```text
CyberTEK{02_May_2026:04:19:40}
```

---

## 4. Farfouch — MITRE Initial Access

**Question:**  
Initial access was achieved through a vulnerable public-facing application.

Identify the MITRE ATT&CK technique ID that describes this initial access method.

**Flag format:** `CyberTEK{TXXXX}`

**Flag:**  
```text
CyberTEK{T1190}
```

---

## 5. n0v4 lm4y3t — Webshell Discovery

**Question:**  
After gaining access, the attacker left behind a webshell on the OFBiz server.

Identify the filename of the webshell dropped by the attacker.

**Flag format:** `CyberTEK{file.extension}`

**Flag:**  
```text
CyberTEK{health.jsp}
```

---

## 6. Samyyy Jhinnn — Reverse Shell Timestamp

**Question:**  
The attacker triggered a reverse shell during the intrusion.

Determine the time at which the reverse shell was triggered.

**Flag format:** `CyberTEK{HH:MM}`

**Flag:**  
```text
CyberTEK{04:19}
```

---

## 7. sno9yy — MITRE Execution

**Question:**  
The attacker used command execution through scripting during the compromise.

Identify the MITRE ATT&CK technique ID that covers the scripting interpreter execution observed in this attack.

**Flag format:** `CyberTEK{TXXXX}`

**Flag:**  
```text
CyberTEK{T1059}
```

---

## 8. Zioudi 21/3 — Malware Binary Hash

**Question:**  
A suspicious binary was staged on the compromised server during the attack.

Identify the SHA256 hash of the malicious binary.

**Flag format:** `CyberTEK{sha256}`

**Flag:**  
```text
CyberTEK{313cde2b5085e32f84d2167f3671c0f7234d0402251aa034d7da4e55d2fe412e}
```

---

## 9. taw tweti bouzou — PyInstaller Malware Analysis

**Question:**  
The staged binary appears to be a packaged Python payload.

Recover the original Python filename from the malicious PyInstaller binary.

**Flag format:** `CyberTEK{filename.py}`

**Flag:**  
```text
CyberTEK{implant.py}
```

---

## 10. l5afe2 — C2 Configuration

**Question:**  
The implant contains a hardcoded command-and-control configuration.

Identify the C2 IP address and port embedded in the malicious implant.

**Flag format:** `CyberTEK{IP:PORT}`

**Flag:**  
```text
CyberTEK{192.168.10.37:4444}
```

---

## 11. Jed Mojo Jojo — Exfiltration Password

**Question:**  
The implant authenticates its file exfiltration activity using a hardcoded secret.

Recover the password used by the implant for exfiltration authentication.

**Flag format:** `CyberTEK{password}`

**Flag:**  
```text
CyberTEK{B@mb00_S47e9!!}
```

---

## 12. Seriooooooo — Shellcode Encoder

**Question:**  
A shellcode blob was found alongside the implant.

Identify the Metasploit encoder used to obfuscate the shellcode.

**Flag format:** `CyberTEK{encoder_name}`

**Flag:**  
```text
CyberTEK{x86/shikata_ga_nai}
```

---

## 13. Bady Idird — PAM Privilege Escalation Clue

**Question:**  
During post-exploitation reconnaissance, the attacker identified a suspicious PAM-related privilege escalation clue.

What suspicious PAM module was introduced during the privilege escalation stage?

**Flag format:** `CyberTEK{clue}`

**Flag:**  
```text
CyberTEK{pam_ghostvein.so}
```

---

## 14. 1dh4M — Privilege Escalation CVE

**Question:**  
The privilege escalation evidence points to a Linux-PAM related vulnerability path.

Identify the CVE associated with this privilege escalation path.

**Flag format:** `CyberTEK{CVE-YYYY-NNNN}`

**Flag:**  
```text
CyberTEK{CVE-2025-6020}
```

---

## 15. Blingos — MITRE Privilege Escalation

**Question:**  
The privilege escalation involved PAM modification/backdoor behavior.

Identify the MITRE ATT&CK sub-technique ID that covers the PAM backdoor technique used in this attack.

**Flag format:** `CyberTEK{TXXXX.XXX}`

**Flag:**  
```text
CyberTEK{T1556.003}
```

---

## 16. sbeveee — SSH Backdoor Key

**Question:**  
The attacker planted an SSH key to preserve privileged access on Server 1.

Identify the comment field of the attacker's backdoor SSH key.

**Flag format:** `CyberTEK{comment}`

**Flag:**  
```text
CyberTEK{venomscript@c2.ghostvein.xyz}
```

---

## 17. No!dea — Malicious Systemd Service

**Question:**  
The attacker installed a malicious systemd service for persistence.

Identify the service name. Submit the name without the `.service` extension.

**Flag format:** `CyberTEK{service-name}`

**Flag:**  
```text
CyberTEK{ghostvein-sync}
```

---

## 18. Zyyz 3 — Cron Persistence

**Question:**  
The attacker created a scheduled task to keep the malicious implant running.

Identify the full cron schedule of the attacker's planted cron job on Server 1.

**Flag format:** `CyberTEK{schedule_with_underscores}`

**Flag:**  
```text
CyberTEK{*/5_*_*_*_*}
```

---

## 19. 3afwi — MITRE Persistence

**Question:**  
The persistence mechanism included a cron-based scheduled task.

Identify the MITRE ATT&CK sub-technique ID for cron-based persistence.

**Flag format:** `CyberTEK{TXXXX.XXX}`

**Flag:**  
```text
CyberTEK{T1053.003}
```

---

## 20. 9oub3aaaaa — Shadow Hash Cracking

**Question:**  
The attacker accessed local credential material during the compromise.

Recover the plaintext password for the ofbiz user.

**Flag format:** `CyberTEK{plaintext_password}`

**Flag:**  
```text
CyberTEK{manchestercity}
```

---

## 21. Seraph — Pivot Credentials

**Question:**  
The attacker found credentials on Server 1 that enabled lateral movement.

Identify the file containing the lateral movement credentials and the username used.

**Flag format:** `CyberTEK{filename_username}`

**Flag:**  
```text
CyberTEK{ansible_inventory.ini_dbadmin}
```

---

## 22. Inferno — Pivot Destination

**Question:**  
The attacker used the discovered credentials to move laterally to the database server.

Identify the destination IP and SSH port used for lateral movement.

**Flag format:** `CyberTEK{IP:PORT}`

**Flag:**  
```text
CyberTEK{10.10.5.35:2222}
```

---

## 23. Hadedi — MITRE Lateral Movement

**Question:**  
The attacker used SSH to move laterally from the compromised ERP server to the database server.

Identify the MITRE ATT&CK sub-technique ID that covers SSH-based lateral movement.

**Flag format:** `CyberTEK{TXXXX.XXX}`

**Flag:**  
```text
CyberTEK{T1021.004}
```

---

## 24. Aymen Dahmen — Database Targeted

**Question:**  
After reaching the database server, the attacker interacted with PostgreSQL data.

Identify the name of the PostgreSQL database targeted and dumped by the attacker.

**Flag format:** `CyberTEK{database_name}`

**Flag:**  
```text
CyberTEK{patients_prod}
```

---

## 25. fer9et 3ami — DNS Tunnel Domain

**Question:**  
The attacker used DNS-style traffic to exfiltrate data from the database server.

Identify the domain suffix used for the DNS tunneling activity.

**Flag format:** `CyberTEK{domain.tld}`

**Flag:**  
```text
CyberTEK{ghostvein.xyz}
```

---

## 26. El Bambo — DNS Exfiltration Decoding

**Question:**  
The DNS tunneling activity contains encoded data.

Reconstruct the data hidden in the DNS queries and recover the full PostgreSQL connection string.

**Flag format:** `CyberTEK{connection_string}`

**Flag:**  
```text
CyberTEK{postgresql://dbadmin:GhostDB#Adm1n2026@10.10.5.35:5432/patients_prod}
```

---

## 27. Kakarot — MITRE Exfiltration

**Question:**  
The attacker used DNS-based network activity to move data out of the environment.

Identify the MITRE ATT&CK technique ID that covers DNS-based data exfiltration.

**Flag format:** `CyberTEK{TXXXX.XXX}`

**Flag:**  
```text
CyberTEK{T1048.003}
```

---

## 28. البامبو الساحق — Full ATT&CK Chain

**Question:**  
You have reconstructed the full Operation GhostVein intrusion chain.

Provide the MITRE ATT&CK technique IDs in order for: Initial Access, Execution, Privilege Escalation via PAM backdoor, Persistence via Cron, Lateral Movement via SSH, and Exfiltration over DNS.

**Flag format:** `CyberTEK{TXXXX_TXXXX_TXXXX.XXX_TXXXX.XXX_TXXXX.XXX_TXXXX.XXX}`

**Flag:**  
```text
CyberTEK{T1190_T1059_T1556.003_T1053.003_T1021.004_T1048.003}
```

---

## Author

**Re4perZ3d**
