# Authentication Activity Analysis

*Observed Activity

The investigation focused on Windows authentication events,
particularly failed and successful login activity.

## Relevant MITRE ATT&CK Technique

### T1110 — Brute Force

Repeated failed authentication attempts can be relevant to
brute-force detection and authentication attack monitoring.

## Investigation Evidence

The investigation used Windows Security Events and KQL queries
to examine authentication activity.

Primary event:

- Event ID 4625 — Failed logon

Related event:

- Event ID 4624 — Successful logon

## SOC Analyst Considerations

A SOC analyst should consider:

- Number of failed attempts
- Time between attempts
- Source IP address
- Target account
- Whether a successful login followed failed attempts
- Whether the activity is consistent with expected behavior

