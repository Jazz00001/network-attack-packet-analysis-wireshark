# Wireshark Display Filters

This file contains the display filters used during the packet investigation.

## ICMP Flood Evidence

```text
icmp && ip.dst == 192.168.1.3
```

### Use Case

Shows ICMP packets destined for the victim. Useful for identifying ICMP Echo Request storms.

---

## ICMP Echo Requests Only

```text
icmp.type == 8
```

### Use Case

Shows ICMP Echo Request packets.

---

## ICMP Echo Replies Only

```text
icmp.type == 0
```

### Use Case

Shows ICMP Echo Reply packets.

---

## TCP SYN Flood Evidence

```text
ip.dst == 192.168.1.3 && tcp.flags.syn == 1 && tcp.flags.ack == 0
```

### Use Case

Shows TCP SYN packets sent to the victim without the ACK flag set. Useful for identifying SYN-only flood behavior.

---

## SYN Packets Only

```text
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

### Use Case

Shows all SYN-only packets in the PCAP.

---

## SSH Brute Force Evidence

```text
ip.src == 192.168.1.4 && ip.dst == 192.168.1.3 && tcp.port == 22
```

### Use Case

Shows SSH traffic from the attacker to the victim.

---

## SMB Enumeration Evidence

```text
tcp.port == 139 || tcp.port == 445
```

### Use Case

Shows SMB and NetBIOS-related traffic.

---

## Attacker to Victim Traffic

```text
ip.src == 192.168.1.4 && ip.dst == 192.168.1.3
```

### Use Case

Shows all traffic generated from Kali Linux to Metasploitable 2.

---

## Victim to Attacker Traffic

```text
ip.src == 192.168.1.3 && ip.dst == 192.168.1.4
```

### Use Case

Shows victim responses to attacker traffic.

---

## TCP Reset Packets

```text
tcp.flags.reset == 1
```

### Use Case

Useful when analyzing failed or abruptly closed sessions.

---

## TCP Conversations Between Attacker and Victim

```text
(ip.addr == 192.168.1.4 && ip.addr == 192.168.1.3) && tcp
```

### Use Case

Shows TCP traffic between the two lab machines.
