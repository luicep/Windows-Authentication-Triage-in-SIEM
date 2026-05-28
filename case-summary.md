# Case Summary

## Scenario

Windows Security authentication events from the public BOTS v3 dataset were reviewed in Splunk to identify failed-logon activity and determine whether the pattern supported escalation.

## Objective

Determine whether the observed failed logons indicate benign low-volume authentication failures, account lockout, brute-force behavior, password spraying, or activity requiring escalation.

## Data Source

| Source | Details |
|---|---|
| Dataset | Splunk BOTS v3 |
| Index | `botsv3` |
| Sourcetype | `WinEventLog:Security` |
| Time Range | All time |
| Event IDs Reviewed | `4624`, `4625`, `4740` |

## Key Evidence

| Evidence | Result |
|---|---|
| Dataset loaded | `2,083,056` events in `botsv3` |
| Successful logons | `427` EventCode `4624` events |
| Failed logons | `3` EventCode `4625` events |
| Account lockouts | No EventCode `4740` observed |
| Affected hosts | `SEPM`, `MKRAEUS-L` |
| Timeline | Low-volume activity across two hourly buckets |

## Final Decision

Low-volume failed-logon activity observed. No confirmed brute-force, password-spray, or account-lockout pattern identified.

## Business / User Impact

In a production environment, failed logons can indicate user access issues, stale credentials, service-account problems, or early signs of credential attack activity. This case did not show enough volume or pattern evidence to justify escalation as a confirmed attack.

## Recommended Action

Document the activity, review involved hosts and logon types, and monitor for additional failed logons, lockouts, or successful logons following failures.
