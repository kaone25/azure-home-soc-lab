# Failed Login Investigation

## Objective

Investigate Windows authentication events collected from the
Azure honeypot VM through Microsoft Sentinel.

## Data Source

Windows Security Events collected through the Microsoft Sentinel
Windows Security Events connector.

## Investigation Query

```kql
SecurityEvents
| where EventID == 4625
| sort by TimeGenerated desc
