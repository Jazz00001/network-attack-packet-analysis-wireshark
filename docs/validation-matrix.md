# Validation Matrix

| Detection ID | Attack Type | Tool Used | Command / Feature | Wireshark Evidence | Expected Result | Status |
|---|---|---|---|---|---|---|
| `DET-001` | ICMP Baseline | ping | `ping -c 5 192.168.1.3` | ICMP Echo Request/Reply | Connectivity confirmed | Verified |
| `DET-002` | ICMP Flood | ping flood | `sudo timeout 8 ping -f 192.168.1.3` | `icmp && ip.dst == 192.168.1.3` | Dense Echo Request stream | Verified |
| `DET-003` | TCP SYN Flood | hping3 | `hping3 -S -p 80 --flood` | `tcp.flags.syn == 1 && tcp.flags.ack == 0` | Repeated SYN-only traffic | Verified |
| `DET-004` | SSH Brute Force | Hydra | `hydra -l msfadmin -P pass.txt -t 4 ssh://192.168.1.3` | `tcp.port == 22` | Repeated short SSH sessions | Verified |
| `DET-005` | SMB Enumeration | Nmap NSE | `nmap -sS -p 139,445 --script smb-os-discovery` | `tcp.port == 139 || tcp.port == 445` | SMB session setup and discovery traffic | Verified |
| `DET-006` | Conversation Review | Wireshark | Statistics -> Conversations | TCP conversation table | Multiple short-lived flows | Verified |

## Validation Notes

The validation approach relies on protocol behavior, not just tool output. This is important because in real incident response, analysts often receive a PCAP without knowing exactly what tool generated the traffic.

## Evidence Confidence

| Detection | Confidence | Reason |
|---|---|---|
| ICMP Flood | High | High-rate Echo Requests are visible |
| SYN Flood | High | SYN-only packets are directly observable |
| SSH Brute Force | Medium-High | SSH payload is encrypted, but repeated session behavior is strong evidence |
| SMB Enumeration | Medium-High | SMB session setup and short query behavior support enumeration |
| Conversations | Medium | Supports findings but is not a standalone detection |
