# Defensive Recommendations

## ICMP Flood Protection

Recommended controls:

- Apply ICMP rate limiting.
- Disable unnecessary ICMP responses from public-facing systems.
- Monitor ICMP traffic volume by source.
- Alert on sudden spikes in Echo Requests.
- Use firewall rules to restrict ICMP from untrusted networks.

## TCP SYN Flood Protection

Recommended controls:

- Enable SYN cookies.
- Tune TCP backlog settings.
- Apply SYN rate limiting.
- Monitor high SYN-to-ACK imbalance.
- Use network IDS signatures for SYN flood behavior.
- Use DDoS protection for internet-facing services.

## SSH Brute-Force Protection

Recommended controls:

- Disable password authentication.
- Use SSH key-based authentication.
- Restrict SSH to trusted IP ranges.
- Use fail2ban or Wazuh active response.
- Alert on repeated SSH login attempts.
- Enforce MFA for remote administrative access where possible.
- Place SSH behind VPN or a bastion host.

## SMB Enumeration Protection

Recommended controls:

- Disable SMB where not required.
- Block ports `139` and `445` from untrusted networks.
- Disable anonymous SMB enumeration.
- Apply least privilege on SMB shares.
- Monitor SMB session setup bursts.
- Segment internal systems that require SMB.
- Alert on Nmap-like SMB enumeration patterns.

## SOC Monitoring Recommendations

Create alerts for:

- High ICMP Echo Request rate.
- SYN-only packet spikes.
- Repeated SSH connections from the same source IP.
- SMB connection attempts to `139` and `445`.
- Multiple short-lived connections from a single host.
- Traffic pattern changes from baseline.

## Incident Response Recommendations

When these patterns are detected:

1. Identify the source IP.
2. Confirm whether the traffic is authorized.
3. Check firewall and endpoint logs.
4. Review authentication logs for SSH attempts.
5. Block or rate-limit malicious source if needed.
6. Preserve PCAP evidence.
7. Document IOCs and timeline.
8. Review exposed services.
