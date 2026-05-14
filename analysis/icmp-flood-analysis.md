# ICMP Flood Analysis

## Detection ID

`DET-002`

## Attack Type

ICMP Flood / ICMP Echo Request Storm

## Objective

Identify high-volume ICMP Echo Request traffic directed from the attacker machine to the victim machine.

## Lab Context

| Role | IP Address |
|---|---:|
| Attacker | `192.168.1.4` |
| Victim | `192.168.1.3` |

## Command Used

```bash
sudo timeout 8 ping -f 192.168.1.3
```

## Wireshark Display Filter

```text
icmp && ip.dst == 192.168.1.3
```

## Packet-Level Evidence

The filtered packet list should show repeated ICMP Echo Request packets from the attacker to the victim.

Expected packet fields:

| Field | Expected Value |
|---|---|
| Source IP | `192.168.1.4` |
| Destination IP | `192.168.1.3` |
| Protocol | ICMP |
| ICMP Type | `8` |
| ICMP Code | `0` |
| Direction | Attacker to Victim |
| Behavior | High-rate repeated Echo Requests |

## Why This Indicates an ICMP Flood

A normal ping test usually sends a small number of packets at predictable intervals. In this case, flood mode generates packets as quickly as the system can send them. The result is a dense sequence of Echo Requests with very short inter-arrival times.

The key evidence is not one packet by itself. The evidence is the repeated high-rate pattern of ICMP Echo Requests sent to the same destination over a short period.

## Screenshot to Add

Save the screenshot as:

```text
screenshots/05-icmp-flood-wireshark-filter.png
```

The screenshot should show:

- The display filter bar.
- Packet list with many ICMP Echo Requests.
- Packet details expanded to show ICMP Type `8`.
- Source IP `192.168.1.4`.
- Destination IP `192.168.1.3`.

## Investigation Notes

The ICMP flood is a network availability attack pattern. In a real environment, this behavior could indicate denial-of-service activity, misconfigured monitoring, or a host generating abnormal diagnostic traffic.

## Defensive Recommendations

- Apply ICMP rate limiting at the firewall.
- Monitor ICMP packet rate per source.
- Alert on high ICMP Echo Request volume to internal assets.
- Restrict ICMP from untrusted sources where possible.
- Use baseline traffic patterns to avoid false positives.

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Impact | Network Denial of Service | `T1498` |

## Conclusion

The filtered traffic is consistent with an ICMP flood because the capture shows a continuous, high-rate stream of ICMP Echo Requests from the attacker to the victim.
