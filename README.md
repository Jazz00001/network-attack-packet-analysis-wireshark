# Advanced Network Attack Packet Analysis Lab — Wireshark, tcpdump, Kali Linux & Metasploitable 2

## Project Overview

This project is an advanced network packet analysis and traffic forensics lab focused on identifying common attack patterns inside packet captures using Wireshark and tcpdump.

The lab simulates multiple offensive activities in a fully isolated VirtualBox environment and then analyzes the captured traffic at packet level. The objective is to demonstrate practical blue-team skills in packet inspection, attack identification, traffic filtering, protocol analysis, and incident documentation.

The attacks analyzed in this project include:

- ICMP flood / ping flood
- TCP SYN flood
- SSH brute-force login attempts
- SMB enumeration and scanning
- TCP conversation analysis using Wireshark statistics

This project is designed for SOC Analyst, Cybersecurity Analyst, Network Security Analyst, and Blue Team portfolio development.

---

## Lab Objective

The objective of this project is to capture malicious network traffic in a controlled lab and perform packet-level investigation using Wireshark.

The project answers the following questions:

1. Can ICMP flood traffic be identified from packet volume and ICMP fields?
2. Can SYN flood behavior be detected using TCP flag analysis?
3. Can SSH brute-force activity be identified even when credentials are encrypted?
4. Can SMB enumeration be distinguished from normal SMB usage?
5. Can Wireshark statistics support attack identification using conversation volume and short-lived flows?

---

## Lab Environment

| Role | Machine | IP Address | Purpose |
|---|---|---|---|
| Attacker | Kali Linux | 192.168.1.4 | Generates attack and scan traffic |
| Victim | Metasploitable 2 | 192.168.1.3 | Vulnerable target machine |
| Analysis Tool | Wireshark | Offline PCAP Analysis | Packet inspection and evidence collection |
| Capture Tool | tcpdump | Kali Linux | Captures traffic into PCAP format |
| Virtualization | Oracle VirtualBox | Host-only/Internal network | Isolated lab environment |

---

## Network Topology

```text
+------------------------+              +-----------------------------+
| Kali Linux Attacker    |              | Metasploitable 2 Victim     |
| IP: 192.168.1.4        | -----------> | IP: 192.168.1.3             |
| Tools: ping, hping3,   |              | Services: SSH, SMB, HTTP    |
| hydra, nmap, tcpdump   |              |                             |
+------------------------+              +-----------------------------+
              |
              v
+------------------------+
| Wireshark Analysis     |
| PCAP: restart_partB_lab.pcap |
+------------------------+
```
