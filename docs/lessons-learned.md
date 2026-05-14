# Lessons Learned

## Technical Lessons

This project strengthened understanding of packet-level network behavior, especially how different attacks appear inside a PCAP.

Key lessons:

- ICMP flood traffic is identified by volume and repeated Echo Request behavior.
- SYN flood traffic is identified through TCP flag patterns.
- SSH brute-force activity can be detected even when payloads are encrypted.
- SMB enumeration can be identified through short discovery-style SMB sessions.
- Wireshark Conversations helps validate traffic volume and flow behavior.
- A packet capture can support incident reporting when evidence is documented clearly.

## Analyst Lessons

The most important lesson is that packet analysis requires both field-level inspection and behavioral interpretation. A single packet may not prove an attack, but repeated patterns across time can provide strong evidence.

## Documentation Lessons

Professional GitHub projects should not only show screenshots. They should explain:

- What was tested.
- Why it matters.
- How evidence was captured.
- Which fields prove the finding.
- What defenders should do about it.
- How the behavior maps to MITRE ATT&CK.

## Future Improvements

- Add Suricata alerts from the same PCAP.
- Add Zeek logs for protocol-level summaries.
- Add Wazuh integration for SIEM visibility.
- Add custom detection rules.
- Add a timeline of attack events.
- Add packet count metrics from Wireshark Statistics.
