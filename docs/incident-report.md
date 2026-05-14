# Incident Report

## Executive Summary

A controlled packet capture was analyzed to identify multiple simulated network attacks against an intentionally vulnerable host. The investigation confirmed ICMP flood traffic, TCP SYN flood behavior, SSH brute-force activity, and SMB enumeration. Evidence was collected using Wireshark filters, packet-level inspection, and conversation statistics.

## Environment

| System | IP Address | Role |
|---|---:|---|
| Kali Linux | `192.168.1.4` | Attacker |
| Metasploitable 2 | `192.168.1.3` | Victim |

## Confirmed Findings

### Finding 1: ICMP Flood

A high volume of ICMP Echo Request packets was observed from `192.168.1.4` to `192.168.1.3`. The traffic showed repeated Type `8`, Code `0` ICMP packets and very short inter-arrival times.

**Severity:** Medium  
**Impact:** Potential bandwidth or CPU exhaustion.

### Finding 2: TCP SYN Flood

Repeated SYN-only packets were observed targeting TCP port `80` on the victim. The traffic showed SYN set and ACK not set, indicating connection initiation without normal handshake completion.

**Severity:** High  
**Impact:** Potential service degradation or half-open connection exhaustion.

### Finding 3: SSH Brute Force

Multiple short-lived SSH sessions were observed from the attacker to TCP port `22` on the victim. Although SSH credentials were encrypted, the repeated session pattern was consistent with brute-force behavior.

**Severity:** High  
**Impact:** Potential credential compromise.

### Finding 4: SMB Enumeration

SMB traffic on ports `139` and `445` was observed. The traffic pattern was consistent with SMB discovery and enumeration rather than normal file transfer.

**Severity:** Medium  
**Impact:** Information disclosure and preparation for further exploitation.

## Indicators

| Type | Value |
|---|---|
| Attacker IP | `192.168.1.4` |
| Victim IP | `192.168.1.3` |
| SSH Port | `22/TCP` |
| HTTP Port | `80/TCP` |
| SMB Ports | `139/TCP`, `445/TCP` |
| Protocol | ICMP |
| Tools | ping, hping3, Hydra, Nmap |

## Timeline Summary

| Phase | Activity |
|---|---|
| Phase 1 | Connectivity verified with ICMP baseline ping |
| Phase 2 | ICMP flood generated |
| Phase 3 | SMB enumeration performed |
| Phase 4 | SSH brute-force attempts generated |
| Phase 5 | SYN flood generated |
| Phase 6 | PCAP analyzed in Wireshark |

## Recommendations

- Rate-limit ICMP.
- Enable SYN flood protection.
- Disable password-based SSH authentication.
- Restrict SSH access to trusted IPs.
- Monitor repeated SSH login attempts.
- Restrict SMB access.
- Disable SMB where not needed.
- Deploy SIEM alerts for scan, flood, and brute-force behavior.

## Conclusion

The packet capture contained clear evidence of multiple network attack patterns. The analysis successfully identified each activity using packet-level evidence, Wireshark filters, protocol fields, and supporting conversation statistics.
