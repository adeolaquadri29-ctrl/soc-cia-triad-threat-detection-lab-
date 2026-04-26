CYBERSECURITY INCIDENT REPORT

CIA TRIAD THREAT DETECTION LAB

1. Introduction

This report presents a practical implementation of the CIA Triad (Confidentiality, Integrity, and Availability) through simulated cyber attacks in a controlled SOC environment.

The objective of this project is to demonstrate the detection, analysis, and response to common cyber threats using industry-standard tools.

⸻

2. Lab Environment

The lab environment consists of:

* Attacker Machine: Kali Linux
* Target System 1: Ubuntu Desktop VM (SSH & File Integrity Target)
* Target System 2: Ubuntu Server VM (DoS Simulation Target)
* Monitoring Tools: Wazuh, Suricata, Wireshark
* Defensive Tool: Fail2Ban

⸻

3. Attack Scenarios and Analysis

3.1 Confidentiality Attack (SSH Brute Force)

Target:
Ubuntu Desktop VM

Objective:
Simulate unauthorized access to the system via SSH.

Method:
A brute force attack was launched using Hydra with a custom username and password list.

Command Used:
hydra -L users.txt -P passwords.txt ssh://192.168.0.X -V

Detection:

* Multiple failed login attempts detected in Wazuh
* Suspicious traffic observed in Suricata logs

Response:

* Fail2Ban blocked the attacker’s IP address
* Logs were analyzed for attack patterns

⸻

3.2 Integrity Attack (File Tampering)

Target:
Ubuntu Desktop VM

Objective:
Detect unauthorized modification of critical system files.

Method:

* A monitored file was created in /opt/critical
* Wazuh File Integrity Monitoring (FIM) was enabled
* Scan interval reduced to 60 seconds
* Real-time monitoring enabled

Command Used:
echo “attack test” | sudo tee -a /opt/critical/testfile.txt

Detection:

* Wazuh FIM triggered an alert
* File hash change detected

Response:

* File contents verified locally
* Permissions restored to secure state (root ownership)

⸻

3.3 Availability Attack (DoS Simulation)

Target:
Ubuntu Server VM

Objective:
Simulate a Denial-of-Service attack affecting system availability.

Method:
A SYN flood attack was performed using hping3.

Command Used:
sudo hping3 -S -p 80 192.168.0.126

Analysis:

* Wireshark captured a high volume of SYN packets
* Filter applied: tcp.flags.syn == 1 && tcp.flags.ack == 0

Detection:

* Abnormal traffic patterns observed

⸻

4. Detection and Monitoring

Wazuh

* Detected brute force attacks on Ubuntu Desktop
* Generated file integrity alerts for monitored files

Suricata

* Logged suspicious network activity during attacks

Wireshark

* Provided packet-level visibility of SYN flood traffic

⸻

5. Incident Response

* Attacker IP blocked using Fail2Ban
* Logs reviewed using Wazuh dashboard
* File integrity restored after tampering
* System stability verified after DoS simulation

⸻

6. MITRE ATT&CK Mapping

* Brute Force Attack → T1110
* File Modification → T1565
* Denial of Service → T1499

⸻

7. Lessons Learned

* Real-time monitoring significantly improves detection speed
* File integrity monitoring is essential for detecting tampering
* Network traffic analysis helps identify abnormal behavior
* Proper system hardening reduces attack surface

⸻

8. Skills Acquired

* SIEM Monitoring and Analysis (Wazuh)
* Network Traffic Analysis (Wireshark)
* Intrusion Detection (Suricata)
* Incident Response and Log Analysis
* Threat Simulation using Kali Linux tools

⸻

9. Conclusion

This project successfully demonstrated the implementation of the CIA Triad in a multi-system cybersecurity lab environment. By simulating attacks across both endpoint and server systems, it highlights the importance of monitoring, detection, and response in maintaining system security.
