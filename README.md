Enterprise Log Monitoring & Threat Detection System (CIA Triad in Practice)

📌 Overview

This project demonstrates the practical implementation of the CIA Triad (Confidentiality, Integrity, and Availability) using a SOC-based home lab.

Real-world cyber attacks were simulated using Kali Linux and detected using Wazuh, Suricata, and Wireshark across multiple target systems.

⸻

🏗️ Lab Architecture

* Attacker Machine: Kali Linux
* Target System 1: Ubuntu Desktop VM (SSH & File Integrity Target)
* Target System 2: Ubuntu Server VM (Web Server – DoS Target)
* Monitoring Tools: Wazuh, Suricata, Wireshark
* Defensive Tool: Fail2Ban
⸻

🛠️ Tools Used

* Wazuh (SIEM & Log Monitoring)
* Suricata (Intrusion Detection System)
* Wireshark (Packet Analysis)
* Hydra (Brute Force Tool)
* hping3 (DoS Simulation Tool)
* Fail2Ban (Intrusion Prevention)

⸻

⚔️ Attack Scenarios

🔒 1. Confidentiality Attack (SSH Brute Force)

🎯 Target:

Ubuntu Desktop VM

🎯 Objective:

Simulate unauthorized access via SSH.

🧰 Tool:

Hydra (Kali Linux)

💻 Command:

hydra -L users.txt -P passwords.txt ssh://192.168.0.X -V

🔍 Detection:

* Wazuh detected multiple failed SSH login attempts
* Suricata logged suspicious traffic
* Fail2Ban blocked attacker IP

⸻

🧾 2. Integrity Attack (File Tampering)

🎯 Target:

Ubuntu Desktop VM

🎯 Objective:

Detect unauthorized modification of monitored files.

⚙️ Setup:

* Created monitored directory: /opt/critical
* Enabled Wazuh File Integrity Monitoring (FIM)
* Reduced scan interval to 60 seconds
* Enabled real-time monitoring

💻 Attack Command:

echo “attack test” | sudo tee -a /opt/critical/testfile.txt

🔍 Detection:

* Wazuh triggered FIM alert
* File hash change detected

🛡️ Response:

* Verified file integrity locally
* Restored secure permissions (root ownership)
⸻

🌐 3. Availability Attack (DoS Simulation)

🎯 Target:

Ubuntu Server VM

🎯 Objective:

Simulate service disruption using SYN flood.

🧰 Tool:

hping3

💻 Command:

sudo hping3 -S -p 80 192.168.0.126

📊 Analysis:

* Wireshark captured high volume SYN packets
* Filter used:
    tcp.flags.syn == 1 && tcp.flags.ack == 0

🔍 Detection:

* Abnormal traffic patterns observed

🔍 Detection & Analysis

Wazuh

* Detected brute force attempts on Ubuntu Desktop
* Triggered file integrity alerts

Suricata

* Logged suspicious network activity

Wireshark

* Visualized SYN flood traffic patterns

⸻

🛡️ Incident Response

* Blocked attacker IP using Fail2Ban
* Monitored alerts via Wazuh dashboard
* Restored file permissions after integrity breach
* Verified system stability after DoS simulation

⸻

🧠 MITRE ATT&CK Mapping

* Brute Force → T1110
* File Modification → T1565
* Denial of Service → T1499

⸻

📚 Lessons Learned

* Real-time monitoring significantly improves detection speed
* File integrity monitoring is essential for detecting tampering
* Network traffic analysis helps identify abnormal behavior
* Proper system hardening reduces attack surface

⸻

💡 Skills Gained

* SIEM Monitoring (Wazuh)
* Network Traffic Analysis (Wireshark)
* Intrusion Detection (Suricata)
* Incident Response
* Threat Simulation using Kali Linux

⸻

⚙️ Setup Guide

See the setup-guide/installation.md file for full environment setup.

⸻

📄 Full Report

See REPORT.md for detailed technical documentation.

⸻

🚀 Conclusion

This project demonstrates hands-on experience in detecting and responding to cyber threats across multiple systems in a SOC environment using industry-standard tools.
