# Escalation Note

## Summary

Windows failed-logon activity was reviewed in Splunk using BOTS v3 Windows Security logs.

The reviewed evidence showed low-volume failed-logon activity across two hosts: `SEPM` and `MKRAEUS-L`.

## Evidence Reviewed

| Evidence | Result |
|---|---|
| Index | `botsv3` |
| Sourcetype | `WinEventLog:Security` |
| Successful logons | `427` EventCode `4624` events |
| Failed logons | `3` EventCode `4625` events |
| Account lockouts | No EventCode `4740` observed |
| Hosts involved | `SEPM`, `MKRAEUS-L` |

## Assessment

The failed-logon activity does not show enough volume or pattern evidence to confirm brute-force activity, password spraying, or account lockout.

The activity should be treated as low-volume authentication triage.

## Escalation Criteria Not Met

- No high-volume failed-logon burst observed
- No account lockout event identified
- No confirmed password-spray pattern
- No large-scale multi-user targeting observed

## Recommended Follow-Up

If this were a production environment, the next team should:

1. Review `SEPM` Logon Type `5` for service-related authentication context.
2. Review `MKRAEUS-L` Logon Type `3` for network logon context.
3. Check for successful logons after failures.
4. Monitor for repeated failed logons or account lockouts.
5. Escalate if volume increases, privileged accounts are involved, or multiple users are targeted.

## Escalation Decision

No immediate escalation recommended based on the reviewed evidence.
