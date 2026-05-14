# TCP SYN Flood Analysis

## Detection ID

`DET-003`

## Attack Type

TCP SYN Flood / Half-Open Connection Exhaustion

## Objective

Identify SYN-only traffic targeting the victim without normal TCP handshake completion.

## Lab Context

| Role | IP Address |
|---|---:|
| Attacker | `192.168.1.4` |
| Victim | `192.168.1.3` |

## Command Used

```bash
sudo timeout 8 hping3 -S -p 80 --flood 192.168.1.3
```

## Wireshark Display Filter

```text
ip.dst == 192.168.1.3 && tcp.flags.syn == 1 && tcp.flags.ack == 0
```

## Packet-Level Evidence

Expected packet fields:

| Field | Expected Value |
|---|---|
| Destination IP | `192.168.1.3` |
| Destination Port | `80` |
| TCP SYN Flag | Set |
| TCP ACK Flag | Not set |
| Source Ports | Multiple ephemeral ports |
| Behavior | Repeated connection initiation attempts |

## Normal TCP Handshake

A normal TCP connection uses this sequence:

```text
Client -> Server: SYN
Server -> Client: SYN/ACK
Client -> Server: ACK
```

## Why This Indicates a SYN Flood

The capture shows many SYN-only packets. SYN-only packets are normal at the beginning of a TCP connection, but a large burst of them without corresponding completed handshakes indicates abnormal behavior.

The repeated SYN packets suggest the attacker is attempting to create many half-open connection states on the victim service.

## Screenshot to Add

Save the screenshot as:

```text
screenshots/06-syn-flood-wireshark-filter.png
```

The screenshot should show:

- The SYN flood display filter.
- Many packets with SYN set and ACK not set.
- Destination IP `192.168.1.3`.
- Destination port `80`.
- TCP flags expanded in packet details.

## Investigation Notes

SYN flood traffic can impact availability by consuming connection resources. In a real network, this traffic may appear as a spike in SYN packets, a low handshake completion ratio, or increased server connection backlog usage.

## Defensive Recommendations

- Enable SYN cookies.
- Apply SYN rate limiting.
- Tune TCP backlog settings.
- Monitor SYN-to-SYN/ACK-to-ACK ratios.
- Use IDS/SIEM rules for abnormal SYN-only volume.
- Place public services behind load balancers or DDoS protection where appropriate.

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Impact | Endpoint Denial of Service | `T1499` |

## Conclusion

The capture supports SYN flood identification because it contains a high volume of SYN-only packets targeting the victim, with no normal completed handshake pattern at the same rate.
