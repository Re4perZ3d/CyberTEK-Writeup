# Operation GhostVein — DFIR Writeup

## 🎮 Play the Challenge

The original DFIR evidence package is still available for anyone who wants to try the scenario before reading the writeup:

📦 **Download evidence:**  
https://drive.google.com/file/d/1qJgTznQsHkGdYdmBSUG38QxmaHtQadZ2/view?usp=sharing

> ⚠️ **Recommendation:** Try solving the challenge first before reading the writeup, as this repository contains full spoilers and flags.

## 🧠 Challenge Questions

The original challenge questions, flag formats, and final flags are available here:

➡️ [View challenge questions](questions/challenges.md)

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

> Replace this README with your exported Notion README if you already have the screenshots locally. Keep the Play/Questions sections above at the top.
