# Methodology

## Project Purpose

The purpose of this project is to perform packet-level analysis of controlled attack traffic inside a safe lab environment. The project focuses on identifying attacks from network evidence instead of relying only on tool output.

## Lab Design

The lab used two virtual machines on the same isolated network segment.

| Machine | Role | IP Address |
|---|---|---:|
| Kali Linux | Attacker | `192.168.1.4` |
| Metasploitable 2 | Victim | `192.168.1.3` |

The network was isolated so the generated attack traffic did not affect any external systems.

## Capture Method

Traffic was captured on Kali Linux using tcpdump.

```bash
sudo tcpdump -i eth0 -nn -s0 -w restart_partB_lab.pcap
```

The `-s0` option captured full packets, the `-w` option wrote the output to a PCAP file, and the `-nn` option prevented name resolution so the analysis remained consistent.

## Attack Generation

The following controlled traffic types were generated:

| Attack | Tool |
|---|---|
| ICMP baseline | ping |
| ICMP flood | ping flood mode |
| TCP SYN flood | hping3 |
| SSH brute force | Hydra |
| SMB enumeration | Nmap NSE |

## Analysis Method

The PCAP file was opened in Wireshark. For each attack category, the analysis followed this workflow:

1. Apply a narrow display filter.
2. Select representative packets.
3. Inspect packet details.
4. Validate protocol fields.
5. Check timing and repeated behavior.
6. Use Wireshark statistics for supporting evidence.
7. Capture screenshots.
8. Document findings and conclusions.

## Evidence Handling

Each finding is documented with:

- Display filter.
- Source and destination IPs.
- Protocol fields.
- Behavioral indicators.
- Screenshot location.
- MITRE ATT&CK mapping.
- Defensive recommendations.

## Scope Limitation

This project is based on lab-generated traffic. It does not represent a full enterprise production network. However, the packet analysis process is transferable to real-world SOC and incident response investigations.
