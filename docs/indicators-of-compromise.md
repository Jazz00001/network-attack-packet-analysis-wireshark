# Indicators of Compromise

## Network Indicators

| Indicator Type | Value | Description |
|---|---|---|
| Source IP | `192.168.1.4` | Kali Linux attacker |
| Destination IP | `192.168.1.3` | Metasploitable 2 victim |
| Protocol | ICMP | Used during baseline ping and ICMP flood |
| TCP Port | `22` | SSH brute-force target |
| TCP Port | `80` | SYN flood target |
| TCP Port | `139` | NetBIOS/SMB |
| TCP Port | `445` | SMB over TCP |

## Behavioral Indicators

| Behavior | Possible Meaning |
|---|---|
| Dense ICMP Echo Request stream | ICMP flood |
| High number of SYN-only packets | SYN flood |
| Many short SSH sessions | Brute-force login attempt |
| SMB session setup bursts | SMB enumeration |
| Multiple short-lived TCP conversations | Scanning or brute-force behavior |

## Tool Indicators

| Tool | Associated Activity |
|---|---|
| ping flood mode | ICMP flood |
| hping3 | SYN flood |
| Hydra | SSH brute force |
| Nmap NSE | SMB enumeration |

## Detection Ideas

| Indicator | Detection Logic |
|---|---|
| ICMP flood | Alert when ICMP Echo Requests exceed baseline threshold |
| SYN flood | Alert when SYN count greatly exceeds completed handshakes |
| SSH brute force | Alert on repeated SSH sessions from one source |
| SMB enumeration | Alert on short SMB sessions to ports `139` and `445` |
