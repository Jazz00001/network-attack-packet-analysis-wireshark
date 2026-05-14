# Wireshark Conversations and Statistics Analysis

## Detection ID

`DET-006`

## Objective

Use Wireshark statistics as supporting evidence for the attack findings.

## Wireshark Feature Used

```text
Statistics -> Conversations -> TCP
```

Optional additional views:

```text
Statistics -> Protocol Hierarchy
Statistics -> Endpoints
Statistics -> I/O Graphs
```

## Why Conversations Matter

Packet filters are useful for isolating specific evidence. Wireshark Conversations provides a wider view of communication patterns between endpoints. It helps validate whether the traffic was isolated, repeated, high-volume, or short-lived.

## Expected Evidence

The Conversations view should show:

| Evidence | Interpretation |
|---|---|
| Multiple TCP conversations | Supports scanning and brute-force activity |
| Repeated flows between `192.168.1.4` and `192.168.1.3` | Confirms attacker-victim pair |
| Short-lived sessions | Supports SSH brute-force and enumeration |
| High packet/byte count for certain flows | Supports flood or scan bursts |
| Multiple destination ports | Supports multi-technique attack simulation |

## Screenshot to Add

Save the screenshot as:

```text
screenshots/09-wireshark-conversations.png
```

The screenshot should show:

- TCP Conversations tab.
- Conversations involving `192.168.1.4` and `192.168.1.3`.
- Packet and byte counts.
- Multiple ports if visible.

## Additional Screenshot

Save Protocol Hierarchy as:

```text
screenshots/10-protocol-hierarchy.png
```

This screenshot should show the protocol distribution inside the PCAP, such as ICMP, TCP, SSH, and SMB-related traffic.

## Analyst Interpretation

The conversations view does not replace packet-level evidence. Instead, it supports the investigation by confirming traffic volume, flow count, and repeated communication between the same hosts.

## Conclusion

Wireshark Conversations supports the overall findings by showing multiple transient TCP flows and abnormal communication patterns between the attacker and victim systems.
