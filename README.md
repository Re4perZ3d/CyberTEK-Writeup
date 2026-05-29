# Operation GhostVein — DFIR Writeup

> ⚠️ **Spoiler Warning:** This writeup contains full solution details and flags for the Operation GhostVein / CyberTEK DFIR challenge.

> A realistic Linux forensic investigation challenge focused on host artifacts, PCAP analysis, malware reversing, persistence, lateral movement, and DNS exfiltration.

---

## 📖 Overview

**Operation GhostVein** is a DFIR-oriented forensic challenge simulating a multi-stage attack against a Linux infrastructure.

The investigation was performed from a realistic evidence package containing:

- Full Linux artifacts from **Server 1**
- Full Linux artifacts from **Server 2**
- Network captures from both servers
- A merged incident PCAP
- Malware artifacts staged during the attack

The goal was to reconstruct the full attack chain using host-based artifacts and network evidence.

---

## 🧩 Attack Chain Summary

| Stage | Activity | MITRE ATT&CK |
|---|---|---|
| Initial Access | Apache OFBiz exploitation | `T1190` |
| Execution | Webshell and reverse shell | `T1059` |
| Privilege Escalation | PAM backdoor | `T1556.003` |
| Persistence | Cron job | `T1053.003` |
| Lateral Movement | SSH pivot | `T1021.004` |
| Exfiltration | DNS tunneling | `T1048.003` |

---

## 1. Evidence Integrity

> **Challenge question — Yoo**  
> Welcome to Operation GhostVein.
>
> Download the DFIR evidence handout:
> `https://drive.google.com/file/d/1qJgTznQsHkGdYdmBSUG38QxmaHtQadZ2/view?usp=sharing`
>
> Your first task is to verify the integrity of the archive and submit its SHA256 hash.
>
> Flag format: `CyberTEK{sha256sum}`

The first step was verifying the provided evidence archive.

```bash
sha256sum GhostVein-IR-Collection.zip
```

Result:

```text
624ca5deb58c36080924c1e5bae7cbe3431d4cae5d6883700bf9081ef791737f
```

Flag:

```text
CyberTEK{624ca5deb58c36080924c1e5bae7cbe3431d4cae5d6883700bf9081ef791737f}
```

---

## 2. Initial Access — Apache OFBiz

> **Challenge question — Zyyz 1**  
> The first signs of compromise point toward the public-facing ERP/OFBiz server.
>
> Identify the CVE that was exploited for initial access against the OFBiz server.
>
> Flag format: `CyberTEK{CVE-YYYY-NNNNN}`

The investigation started with the ERP/OFBiz server.

Relevant evidence:

```text
server1/opt/ofbiz/VERSION
server1/opt/ofbiz/BUILD-INFO
server1/var/log/ofbiz/ofbiz.log
server1/var/log/apache2/access.log
```

The server was running **Apache OFBiz 18.12.14**, and the logs showed activity targeting:

```text
/webtools/control/ProgramExport
```

This behavior matched exploitation of:

```text
CVE-2024-38856
```

Flag:

```text
CyberTEK{CVE-2024-38856}
```

---

## 3. First Contact Timestamp

> **Challenge question — Zyyz 2**  
> The attacker touched the OFBiz server before the full compromise chain began.
>
> Determine the timestamp of the attacker's first request to the OFBiz server.
>
> Flag format: `CyberTEK{DD_Mon_YYYY:HH:MM:SS}`

The first attacker request was found in the Apache access logs.

Flag:

```text
CyberTEK{02_May_2026:04:19:40}
```

---

## 4. MITRE Initial Access

> **Challenge question — Farfouch**  
> Initial access was achieved through a vulnerable public-facing application.
>
> Identify the MITRE ATT&CK technique ID that describes this initial access method.
>
> Flag format: `CyberTEK{TXXXX}`

The attack technique maps to **Exploit Public-Facing Application**.

Flag:

```text
CyberTEK{T1190}
```

---

## 5. Webshell Discovery

> **Challenge question — n0v4 lm4y3t**  
> After gaining access, the attacker left behind a webshell on the OFBiz server.
>
> Identify the filename of the webshell dropped by the attacker.
>
> Flag format: `CyberTEK{file.extension}`

A suspicious JSP file was discovered inside the OFBiz web application path.

Flag:

```text
CyberTEK{health.jsp}
```

---

## 6. Reverse Shell Timestamp

> **Challenge question — Samyyy Jhinnn**  
> The attacker triggered a reverse shell during the intrusion.
>
> Determine the time at which the reverse shell was triggered.
>
> Flag format: `CyberTEK{HH:MM}`

The reverse shell callback was identified and correlated with the attack timeline.

Flag:

```text
CyberTEK{04:19}
```

---

## 7. MITRE Execution

> **Challenge question — sno9yy**  
> The attacker used command execution through scripting during the compromise.
>
> Identify the MITRE ATT&CK technique ID that covers the scripting interpreter execution observed in this attack.
>
> Flag format: `CyberTEK{TXXXX}`

The attacker executed commands through an interpreter/webshell path.

Flag:

```text
CyberTEK{T1059}
```

---

## 8. Malware Binary Hash

> **Challenge question — Zioudi 21/3**  
> A suspicious binary was staged on the compromised server during the attack.
>
> Identify the SHA256 hash of the malicious binary.
>
> Flag format: `CyberTEK{sha256}`

A suspicious binary named `monitor` was found on the compromised server.

Flag:

```text
CyberTEK{313cde2b5085e32f84d2167f3671c0f7234d0402251aa034d7da4e55d2fe412e}
```

---

## 9. PyInstaller Malware Analysis

> **Challenge question — taw tweti bouzou**  
> The staged binary appears to be a packaged Python payload.
>
> Recover the original Python filename from the malicious PyInstaller binary.
>
> Flag format: `CyberTEK{filename.py}`

The `monitor` binary was identified as a PyInstaller-packed payload.

Flag:

```text
CyberTEK{implant.py}
```

---

## 10. C2 Configuration

> **Challenge question — l5afe2**  
> The implant contains a hardcoded command-and-control configuration.
>
> Identify the C2 IP address and port embedded in the malicious implant.
>
> Flag format: `CyberTEK{IP:PORT}`

After extraction/decompilation, the implant revealed a hardcoded C2 endpoint.

Flag:

```text
CyberTEK{192.168.10.37:4444}
```

---

## 11. Exfiltration Password

> **Challenge question — Jed Mojo Jojo**  
> The implant authenticates its file exfiltration activity using a hardcoded secret.
>
> Recover the password used by the implant for exfiltration authentication.
>
> Flag format: `CyberTEK{password}`

The implant contained a hardcoded authentication value used during exfiltration.

Flag:

```text
CyberTEK{B@mb00_S47e9!!}
```

---

## 12. Shellcode Encoder

> **Challenge question — Seriooooooo**  
> A shellcode blob was found alongside the implant.
>
> Identify the Metasploit encoder used to obfuscate the shellcode.
>
> Flag format: `CyberTEK{encoder_name}`

A shellcode blob was found alongside the implant and identified as using the following encoder.

Flag:

```text
CyberTEK{x86/shikata_ga_nai}
```

---

## 13. PAM Privilege Escalation Clue

> **Challenge question — Bady Idird**  
> During post-exploitation reconnaissance, the attacker identified a suspicious PAM-related privilege escalation clue.
>
> What suspicious PAM module was introduced during the privilege escalation stage?
>
> Flag format: `CyberTEK{clue}`

A suspicious PAM module was introduced during the privilege escalation stage.

Flag:

```text
CyberTEK{pam_ghostvein.so}
```

---

## 14. Privilege Escalation CVE

> **Challenge question — 1dh4M**  
> The privilege escalation evidence points to a Linux-PAM related vulnerability path.
>
> Identify the CVE associated with this privilege escalation path.
>
> Flag format: `CyberTEK{CVE-YYYY-NNNN}`

The evidence linked the PAM privilege escalation stage to the following CVE.

Flag:

```text
CyberTEK{CVE-2025-6020}
```

---

## 15. MITRE Privilege Escalation

> **Challenge question — Blingos**  
> The privilege escalation involved PAM modification/backdoor behavior.
>
> Identify the MITRE ATT&CK sub-technique ID that covers the PAM backdoor technique used in this attack.
>
> Flag format: `CyberTEK{TXXXX.XXX}`

The attacker modified PAM authentication behavior.

Flag:

```text
CyberTEK{T1556.003}
```

---

## 16. SSH Backdoor Key

> **Challenge question — sbeveee**  
> The attacker planted an SSH key to preserve privileged access on Server 1.
>
> Identify the comment field of the attacker's backdoor SSH key.
>
> Flag format: `CyberTEK{comment}`

The attacker planted an SSH key for persistence.

Flag:

```text
CyberTEK{venomscript@c2.ghostvein.xyz}
```

---

## 17. Malicious Systemd Service

> **Challenge question — No!dea**  
> The attacker installed a malicious systemd service for persistence.
>
> Identify the service name. Submit the name without the `.service` extension.
>
> Flag format: `CyberTEK{service-name}`

A malicious systemd service was installed for persistence.

Flag:

```text
CyberTEK{ghostvein-sync}
```

---

## 18. Cron Persistence

> **Challenge question — Zyyz 3**  
> The attacker created a scheduled task to keep the malicious implant running.
>
> Identify the full cron schedule of the attacker's planted cron job on Server 1.
>
> Flag format: `CyberTEK{schedule_with_underscores}`

The attacker created a cron job to keep the implant running.

Flag:

```text
CyberTEK{*/5_*_*_*_*}
```

---

## 19. MITRE Persistence

> **Challenge question — 3afwi**  
> The persistence mechanism included a cron-based scheduled task.
>
> Identify the MITRE ATT&CK sub-technique ID for cron-based persistence.
>
> Flag format: `CyberTEK{TXXXX.XXX}`

Persistence through cron maps to the following MITRE ATT&CK sub-technique.

Flag:

```text
CyberTEK{T1053.003}
```

---

## 20. Shadow Hash Cracking

> **Challenge question — 9oub3aaaaa**  
> The attacker accessed local credential material during the compromise.
>
> Recover the plaintext password for the ofbiz user.
>
> Flag format: `CyberTEK{plaintext_password}`

The attacker accessed local credential material, including `/etc/passwd` and `/etc/shadow`.

Flag:

```text
CyberTEK{manchestercity}
```

---

## 21. Pivot Credentials

> **Challenge question — Seraph**  
> The attacker found credentials on Server 1 that enabled lateral movement.
>
> Identify the file containing the lateral movement credentials and the username used.
>
> Flag format: `CyberTEK{filename_username}`

The attacker found credentials for lateral movement in an Ansible inventory file.

Flag:

```text
CyberTEK{ansible_inventory.ini_dbadmin}
```

---

## 22. Pivot Destination

> **Challenge question — Inferno**  
> The attacker used the discovered credentials to move laterally to the database server.
>
> Identify the destination IP and SSH port used for lateral movement.
>
> Flag format: `CyberTEK{IP:PORT}`

The lateral movement destination was found in host evidence and PCAP traffic.

Flag:

```text
CyberTEK{10.10.5.35:2222}
```

---

## 23. MITRE Lateral Movement

> **Challenge question — Hadedi**  
> The attacker used SSH to move laterally from the compromised ERP server to the database server.
>
> Identify the MITRE ATT&CK sub-technique ID that covers SSH-based lateral movement.
>
> Flag format: `CyberTEK{TXXXX.XXX}`

The attacker moved laterally using SSH.

Flag:

```text
CyberTEK{T1021.004}
```

---

## 24. Database Targeted

> **Challenge question — Aymen Dahmen**  
> After reaching the database server, the attacker interacted with PostgreSQL data.
>
> Identify the name of the PostgreSQL database targeted and dumped by the attacker.
>
> Flag format: `CyberTEK{database_name}`

After reaching Server 2, the attacker interacted with PostgreSQL.

Flag:

```text
CyberTEK{patients_prod}
```

---

## 25. DNS Tunnel Domain

> **Challenge question — fer9et 3ami**  
> The attacker used DNS-style traffic to exfiltrate data from the database server.
>
> Identify the domain suffix used for the DNS tunneling activity.
>
> Flag format: `CyberTEK{domain.tld}`

DNS-style traffic was used for exfiltration.

Flag:

```text
CyberTEK{ghostvein.xyz}
```

---

## 26. DNS Exfiltration Decoding

> **Challenge question — El Bambo**  
> The DNS tunneling activity contains encoded data.
>
> Reconstruct the data hidden in the DNS queries and recover the full PostgreSQL connection string.
>
> Flag format: `CyberTEK{connection_string}`

The DNS query labels contained encoded data that reconstructed the PostgreSQL connection string.

Flag:

```text
CyberTEK{postgresql://dbadmin:GhostDB#Adm1n2026@10.10.5.35:5432/patients_prod}
```

---

## 27. MITRE Exfiltration

> **Challenge question — Kakarot**  
> The attacker used DNS-based network activity to move data out of the environment.
>
> Identify the MITRE ATT&CK technique ID that covers DNS-based data exfiltration.
>
> Flag format: `CyberTEK{TXXXX.XXX}`

The attacker exfiltrated data over DNS.

Flag:

```text
CyberTEK{T1048.003}
```

---

## 28. Full ATT&CK Chain

> **Challenge question — البامبو الساحق**  
> You have reconstructed the full Operation GhostVein intrusion chain.
>
> Provide the MITRE ATT&CK technique IDs in order for: Initial Access, Execution, Privilege Escalation via PAM backdoor, Persistence via Cron, Lateral Movement via SSH, and Exfiltration over DNS.
>
> Flag format: `CyberTEK{TXXXX_TXXXX_TXXXX.XXX_TXXXX.XXX_TXXXX.XXX_TXXXX.XXX}`

The full chain reconstructed from evidence was:

Flag:

```text
CyberTEK{T1190_T1059_T1556.003_T1053.003_T1021.004_T1048.003}
```

---

## Author

**Re4perZ3d**
