# Detection: Repeated Failed Logons

* Objective

Identify repeated failed authentication attempts that may
require SOC investigation.

* KQL

SecurityEvents
| where EventID == 4625
| summarize FailedAttempts = count() by IpAddress, Account, bin(TimeGenerated, 15m)
| where FailedAttempts >= 5
| sort by FailedAttempts desc
