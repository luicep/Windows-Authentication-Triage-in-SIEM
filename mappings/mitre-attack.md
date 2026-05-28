# MITRE ATT&CK Mapping

## Reviewed Techniques

| Technique | Name | Relevance |
|---|---|---|
| `T1110` | Brute Force | Failed logon activity can indicate brute-force behavior when repeated password attempts are observed against one or more accounts. |
| `T1110.003` | Password Spraying | Failed logons across multiple users from a common source may indicate password spraying. |
| `T1078` | Valid Accounts | Failed logons followed by successful authentication may require review for possible valid credential abuse. |

## Lab Evidence

The reviewed BOTS v3 Windows Security logs contained:

- `427` successful logons
- `3` failed logons
- No observed EventCode `4740` account lockout events
- Failed logons on `SEPM` and `MKRAEUS-L`

## Analyst Assessment

The observed failed-logon activity was low-volume and did not confirm brute-force behavior, password spraying, or valid account abuse.

The techniques listed above were considered during triage because they are relevant to Windows authentication failures, but the available evidence did not meet the threshold for confirmed malicious activity.

## Detection Logic Considered

Potential escalation indicators would include:

- High-volume failed logons against one account
- One source attempting authentication across many users
- Failed logons followed by successful logons
- Failed logons involving privileged accounts
- Account lockout events
- Repeated authentication failures from unusual hosts or sources

## Final Mapping Decision

No ATT&CK technique was confirmed from the reviewed evidence.

This lab demonstrates how a SOC analyst can use MITRE ATT&CK as a triage reference without forcing a malicious conclusion when the evidence does not support it.
