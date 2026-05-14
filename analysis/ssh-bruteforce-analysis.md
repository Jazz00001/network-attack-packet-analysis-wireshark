# SSH Brute-Force Analysis

## Detection ID

`DET-004`

## Attack Type

SSH Brute Force / Repeated Authentication Attempts

## Objective

Identify repeated SSH login attempts from the attacker to the victim using traffic behavior.

## Lab Context

| Role | IP Address |
|---|---:|
| Attacker | `192.168.1.4` |
| Victim | `192.168.1.3` |
| Target Port | `22/TCP` |

## Command Used

```bash
hydra -l msfadmin -P pass.txt -t 4 ssh://192.168.1.3
```

## Wireshark Display Filter

```text
ip.src == 192.168.1.4 && ip.dst == 192.168.1.3 && tcp.port == 22
```

## Packet-Level Evidence

Expected traffic characteristics:

| Evidence | Description |
|---|---|
| TCP port | Repeated connections to `22/TCP` |
| Protocol | SSH |
| SSH banner | SSHv2 negotiation visible |
| Session behavior | Short-lived repeated sessions |
| Connection teardown | FIN/ACK or RST after attempts |
| Timing | Many attempts in a short period |

## Important Analysis Note

SSH encrypts the authentication exchange. This means the attempted passwords are not visible in plaintext inside Wireshark. The detection is therefore based on connection behavior rather than credential visibility.

## Why This Indicates SSH Brute Force

A user logging in normally would usually create one SSH session and keep it open. In this capture, the evidence should show many short SSH sessions occurring close together in time. This is consistent with automated password guessing using a tool such as Hydra.

## Screenshot to Add

Save the screenshot as:

```text
screenshots/07-ssh-bruteforce-wireshark-filter.png
```

The screenshot should show:

- The SSH brute-force filter.
- Repeated traffic to TCP port `22`.
- SSHv2 negotiation in the packet list or packet details.
- Multiple connections between `192.168.1.4` and `192.168.1.3`.

## Investigation Notes

When payloads are encrypted, analysts must rely on metadata and behavioral patterns. This includes connection count, session duration, timing, source/destination pairs, destination ports, and teardown behavior.

## Defensive Recommendations

- Disable SSH password authentication.
- Use SSH keys.
- Restrict SSH access using firewall allowlists.
- Use fail2ban or Wazuh active response.
- Alert on repeated failed SSH attempts.
- Enforce MFA for administrative access where possible.
- Move SSH behind a VPN or bastion host.

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Credential Access | Brute Force | `T1110` |
| Credential Access | Password Guessing | `T1110.001` |

## Conclusion

The capture supports SSH brute-force identification because it shows repeated short-lived SSH sessions from the attacker to the victim. The passwords are encrypted, but the traffic pattern is consistent with automated login attempts.
