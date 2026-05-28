# SOC Triage Ticket

## Alert Summary

Windows failed-logon activity was reviewed in Splunk using the public BOTS v3 dataset.

## Alert Type

Authentication failure / Windows failed logon review

## Data Source

| Field | Value |
|---|---|
| Index | `botsv3` |
| Sourcetype | `WinEventLog:Security` |
| EventCode Reviewed | `4624`, `4625`, `4740` |
| Time Range | All time |

## Key Evidence

| Evidence | Result |
|---|---|
| Total BOTS v3 events | `2,083,056` |
| Successful logons | `427` EventCode `4624` events |
| Failed logons | `3` EventCode `4625` events |
| Account lockouts | No EventCode `4740` observed |
| Hosts with failed logons | `SEPM`, `MKRAEUS-L` |

## Investigation Steps

1. Confirmed the BOTS v3 dataset was loaded into Splunk.
2. Identified Windows Security logs using `WinEventLog:Security`.
3. Reviewed authentication EventCodes `4624`, `4625`, and `4740`.
4. Isolated EventCode `4625` failed-logon events.
5. Grouped failed logons by account, host, and logon type.
6. Reviewed failed-logon timing using a 1-hour timechart.
7. Determined whether the activity supported escalation.

## Findings

Three failed-logon events were identified. The activity was low-volume and occurred across two hosts: `SEPM` and `MKRAEUS-L`.

The failed-logon timeline showed activity across two hourly buckets and did not show a rapid burst.

No account lockout events were observed.

## Analyst Decision

Low-volume failed-logon activity observed. No confirmed brute-force, password-spray, or account-lockout pattern identified.

## Severity

Low

## Recommended Action

- Document the failed-logon activity.
- Review `SEPM` Logon Type `5` for service-related context.
- Review `MKRAEUS-L` Logon Type `3` for network logon context.
- Monitor for additional failed logons, lockouts, or successful logons after failures.

## Ticket Status

Closed as reviewed / no confirmed escalation pattern found.
