# SPL Searches Used

## Dataset Validation

### Confirm BOTS v3 index loaded

```spl
index=*
| stats count by index
| sort - count
```

**Purpose:** Confirm Splunk can search the BOTS v3 dataset and identify the active index.

**Result:** The `botsv3` index returned `2,083,056` events.

---

## Sourcetype Validation

### Identify available sourcetypes

```spl
index=botsv3
| stats count by sourcetype
| sort - count
```

**Purpose:** Review the available log sources in the BOTS v3 dataset.

**Result:** The dataset included Windows Security logs under `WinEventLog:Security`.

---

## Authentication Event Summary

### Count Windows authentication event types

```spl
index=botsv3 sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625 OR EventCode=4740)
| stats count by EventCode
| sort EventCode
```

**Purpose:** Compare successful logons, failed logons, and account lockout events.

**Result:**

| EventCode | Meaning | Count |
|---|---|---:|
| 4624 | Successful logon | 427 |
| 4625 | Failed logon | 3 |

No EventCode `4740` account lockout events were observed in the reviewed scope.

---

## Failed Logon Evidence

### Show Event ID 4625 failed logons

```spl
index=botsv3 sourcetype="WinEventLog:Security" EventCode=4625
| table _time host Account_Name TargetUserName EventCode Logon_Type
```

**Purpose:** Display failed-logon evidence in a compact table for review.

**Result:** Three failed-logon events were identified.

---

## Failed Logons by Account and Host

```spl
index=botsv3 sourcetype="WinEventLog:Security" EventCode=4625
| eval Account=coalesce(Account_Name, user, User, "N/A")
| eval LogonType=coalesce(Logon_Type, LogonType, "N/A")
| eval Host=coalesce(host, ComputerName, "N/A")
| eval Account=if(Account="-", "N/A", Account)
| stats count by Account Host LogonType
| sort - count
```

**Purpose:** Identify which accounts and hosts were associated with failed logons.

**Result:** Failed logons were observed on `SEPM` and `MKRAEUS-L`.

---

## Failed Logon Timeline

```spl
index=botsv3 sourcetype="WinEventLog:Security" EventCode=4625
| timechart span=1h count
```

**Purpose:** Review failed-logon timing to determine whether activity occurred in a burst or across separate time windows.

**Result:** Three failed-logon events appeared across two hourly buckets, indicating low-volume activity rather than a high-volume brute-force pattern.
