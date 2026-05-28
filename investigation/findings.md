# Findings

## Summary

The BOTS v3 dataset was successfully loaded into Splunk and reviewed for Windows authentication activity.

## Key Results

| Area | Finding |
|---|---|
| Index reviewed | `botsv3` |
| Total dataset events | `2,083,056` |
| Time range | All time |
| Successful logons | `427` EventCode `4624` events |
| Failed logons | `3` EventCode `4625` events |
| Account lockouts | No EventCode `4740` events observed |

## Failed Logon Details

| Account | Host | Logon Type | Count |
|---|---|---:|---:|
| N/A | SEPM | 5 | 2 |
| Guest | MKRAEUS-L | 3 | 1 |
| MalloryKrauesen | MKRAEUS-L | 3 | 1 |

## Timeline

The failed-logon timeline showed:

- 2 failed logons around 5:00 AM
- 1 failed logon around 7:00 AM

## Finding

The failed-logon volume was low and did not show a rapid burst, account lockout, or broad multi-account pattern. The evidence supports authentication triage, not a confirmed brute-force or password-spray incident.
