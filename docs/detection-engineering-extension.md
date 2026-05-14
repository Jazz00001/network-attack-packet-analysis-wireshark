# Detection Engineering Extension

## Purpose

This section explains how this packet-analysis project can be extended into a more advanced detection engineering project using tools such as Wazuh, Suricata, Zeek, or Sigma-style logic.

## Why Add This Extension

Wireshark analysis proves that the attack behavior exists in the PCAP. Detection engineering converts that understanding into repeatable monitoring logic.

## Possible Suricata Detection Ideas

### ICMP Flood Logic

```text
Alert when one source sends an abnormal number of ICMP Echo Requests to one destination within a short time window.
```

### SYN Flood Logic

```text
Alert when a high number of SYN packets are observed without corresponding completed handshakes.
```

### SSH Brute Force Logic

```text
Alert when one source creates many SSH sessions to the same destination within a short time window.
```

### SMB Enumeration Logic

```text
Alert when one source attempts SMB connections to ports 139 and 445 with short session duration and enumeration-style behavior.
```

## Possible Wazuh Use Cases

| Use Case | Data Source | Detection Idea |
|---|---|---|
| SSH brute force | `/var/log/auth.log` | Multiple failed SSH attempts |
| SMB enumeration | Network IDS logs | Repeated SMB session attempts |
| SYN flood | Firewall/IDS logs | High SYN packet rate |
| ICMP flood | Network IDS logs | High ICMP packet rate |

## Portfolio Upgrade Plan

To upgrade this project further:

1. Replay the PCAP through Suricata.
2. Generate alerts from the same traffic.
3. Add Suricata alert screenshots.
4. Forward Suricata logs into Wazuh.
5. Build a Wazuh dashboard showing the four attack types.
6. Create detection rules and validation notes.
7. Add a final incident report combining packet and SIEM evidence.

## Advanced Resume Positioning

This extension would allow the project to be described as:

```text
Built a packet-forensics and detection-engineering lab by capturing attack traffic in Wireshark, validating packet-level evidence, replaying PCAPs through IDS tooling, and mapping detections to MITRE ATT&CK.
```
