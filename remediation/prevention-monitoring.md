# Prevention and Monitoring

## Summary

The reviewed evidence showed low-volume failed-logon activity. No confirmed brute-force, password-spray, or account-lockout pattern was identified. Monitoring should focus on detecting when authentication failures increase in volume, affect multiple users, involve privileged accounts, or are followed by successful logons.

## Monitoring Opportunities

| Monitoring Area | Detection Goal |
|---|---|
| Repeated failed logons | Identify possible brute-force attempts |
| Multiple users failing from one source | Identify possible password spraying |
| Failed logons followed by success | Identify possible credential compromise |
| Privileged account failures | Identify risk to administrative access |
| Account lockouts | Identify user impact or repeated password attempts |
| Service account failures | Identify stale credentials or broken scheduled services |

## Example Detection Logic

### High failed-logon volume by account

```spl
index=botsv3 sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name host
| where count >= 10
| sort - count
