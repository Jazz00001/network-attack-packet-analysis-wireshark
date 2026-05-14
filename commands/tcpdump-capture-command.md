# tcpdump Capture Command

## Purpose

This file documents the packet capture process used to collect lab traffic for offline Wireshark analysis. Capturing the traffic at the attacker VM allows all generated attack traffic to be saved into a single PCAP file.

## Interface Confirmation

Before starting capture, confirm the active network interface on Kali Linux:

```bash
ip a
```

Expected attacker IP:

```text
192.168.1.4
```

In this lab, the primary interface was:

```text
eth0
```

## Capture Command

```bash
sudo tcpdump -i eth0 -nn -s0 -w restart_partB_lab.pcap
```

## Explanation

| Option | Meaning |
|---|---|
| `sudo` | Required to capture packets from a network interface |
| `tcpdump` | Packet capture utility |
| `-i eth0` | Captures traffic from the `eth0` interface |
| `-nn` | Disables DNS and port-name resolution |
| `-s0` | Captures the full packet instead of truncating |
| `-w restart_partB_lab.pcap` | Writes raw packets to a PCAP file |

## Why `-nn` Was Used

Using `-nn` keeps the capture deterministic. IP addresses and ports remain visible as raw values instead of being converted into hostnames or service names. This makes evidence documentation cleaner and easier to reproduce.

## Why `-s0` Was Used

The `-s0` flag ensures full packet capture. This is important because truncated packets can remove protocol details needed during Wireshark analysis.

## Output File

```text
restart_partB_lab.pcap
```

Place the final PCAP file in:

```text
pcaps/restart_partB_lab.pcap
```

## Validation

After capture, verify the PCAP file exists:

```bash
ls -lh restart_partB_lab.pcap
```

Optional quick read test:

```bash
tcpdump -nn -r restart_partB_lab.pcap | head
```
