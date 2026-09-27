# Microsoft Sentinel KQL Queries

## 1. View Security Events

```kql
SecurityEvents
| sort by TimeGenerated desc

## 2. View Recent Security Events

SecurityEvents
| where TimeGenerated > ago(24h)
| sort by TimeGenerated desc

## 3. Identify Failed Logons

SecurityEvents
| where EventID == 4625
| sort by TimeGenerated desc

## 4. Identify Successful Logons

SecurityEvents
| where EventID == 4624
| sort by TimeGenerated desc

## 5. Investigate Source IP Addresses

SecurityEvents
| where IpAddress != ""
| summarize EventCount = count() by IpAddress
| sort by EventCount desc
