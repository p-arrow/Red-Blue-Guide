# Blue Team

<br />

## Types
1. Signature based (least false positives)
2. Anomaly based (more false positives): Prescribed patterns (e.g. RFC, industry standards)
3. Behaviour based (most false positives): Patterns that BlueTeam describe themselves

*--> Methods can be combined in some IDS/IPS systems*

## Baselining

*Process of measuring changes in networks, hardware, software etc*

- Windows Tool: Performance Monitor (Perfmon.exe)
- Linux Tool:

*--> Alerts should be configured for automation (!)*

## Port Mirroring (SPAN/Switched Port Analyzer)
- SPAN port is needed for receiving captured traffic (logical device)
- If SPAN port is not possible, network tap is an alternative (physical device)
- Additional load on Switch and CPU though (!)

## Continuous Monitoring
- (+) Situational awareness
- (+) Routine audits
- (+) Realtime analysis
- (+) Proactive posture
- Expensive and complex (!)
- Consumes much ressources (!)

## Monitoring Logs Best Practice
- Stored separately from the server/computer
- Archived
- Backed up
- Encrypted
