# Analyst Decision

## Decision

Low-volume failed-logon activity observed. No confirmed brute-force, password-spray, or account-lockout pattern identified.

## Evidence

- BOTS v3 loaded successfully with `2,083,056` events.
- Windows Security authentication logs contained `427` successful logons and `3` failed logons.
- Failed logons occurred on `SEPM` and `MKRAEUS-L`.
- No EventCode `4740` account lockout events were observed.
- Timeline showed low-volume activity across two hourly buckets.

## What Was Ruled Out

- High-volume brute-force behavior
- Password-spray pattern
- Account lockout
- Large-scale multi-user targeting

## Confidence

Medium.

The evidence supports low-volume authentication failures. Additional endpoint, user, and surrounding log context would be needed before closing or escalating in a production SOC.

## Recommended Action

- Document the failed-logon activity.
- Review `SEPM` Logon Type `5` for service-related context.
- Review `MKRAEUS-L` Logon Type `3` for network logon context.
- Monitor for additional failed logons, lockouts, or successful logons after failures.
