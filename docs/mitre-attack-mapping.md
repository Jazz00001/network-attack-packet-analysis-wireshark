# MITRE ATT&CK Mapping

## Purpose

This file maps observed packet-level behavior to MITRE ATT&CK techniques. The goal is to make the project useful for SOC investigation, alert triage, and resume presentation.

| Observed Activity | Tactic | Technique | ID | Evidence |
|---|---|---|---|---|
| ICMP flood traffic | Impact | Network Denial of Service | `T1498` | High-rate ICMP Echo Requests |
| SYN flood traffic | Impact | Endpoint Denial of Service | `T1499` | Repeated SYN-only packets |
| SSH repeated login attempts | Credential Access | Brute Force | `T1110` | Multiple SSH sessions |
| SSH password guessing | Credential Access | Password Guessing | `T1110.001` | Hydra-style repeated authentication attempts |
| SMB port discovery | Discovery | Network Service Discovery | `T1046` | Nmap scanning ports `139` and `445` |
| SMB host information discovery | Discovery | Remote System Discovery | `T1018` | SMB discovery and session setup |
| Active service probing | Reconnaissance | Active Scanning | `T1595` | Scan-like traffic pattern |

## Analyst Notes

MITRE mapping does not prove an attack by itself. It is used after packet evidence has been reviewed. The PCAP evidence supports these mappings because each technique was observed through protocol fields, port activity, or connection behavior.

## Practical SOC Use

These mappings can be used to build SIEM dashboards, detection rules, incident reports, and analyst playbooks.
