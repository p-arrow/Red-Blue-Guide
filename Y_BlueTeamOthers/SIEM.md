*Security Information Event Management*

## SIEM Software
- ArcSite
- Splunk
- QRadar
- Snort
- ...


## Data Collection Methods
1. Agent-based
   - Service installed on each host to log/filter/norm.
2. Listener/Collector
   - Hosts push updates by using syslog/SNMP
3. Sensors
   - Collect traffic flow data from sniffers across NW

## Best Practice

1. Normalize aggregated data from multiple sources in multiple formats 
2. Synchronization of date/time: UTC (Coordinated Universal Time)
3. Log data must be secured meeting CIA principle
4. Configure dashboard subject to user's role
5. Focus on events related to "need to know" 
6. Develop Use Cases to mitigate risk of false positives 
   - Use Case: specifc condition e.g. suspicious log-on
7. Control & Manage Access to SIEM
8. Evaluate your data sources and alert effectiveness


## Proper KPI's (Key Performance Indicator)

- \# of vulnerabilities
- \# of failed log-ons
- \# of vulnerable systems
- \# of security incidents
- \* Average response time
- \* Average time to resolve tickets
- \# of outstanding issues
- \# of employees trained
- \% of testing completed

## Trend Analysis I
1. Frequency-based: Monitors the number of occurrences over time
2. Volume-based: Metric based on size
- Consider Statistical Deviation (!)
- Consider Sparse Attacks (buried under normal NW noise) (!)

## Trend Analysis II
- Make sure what you want to measure before starting Trend Analysis
   a) Alerts
   b) Network metrics
   c) Time to respond
   d) Education
   e) Compliance

## SIEM Correlation Rule Example

*Error.LogonFailure > 3 AND LogonFailure.User AND Duration < 1 hour*

- This rule would require data in memory for 1 hour (!)
- Instead: SIEM Query
   - Extracts records from all data stored for review or visualization
   - Exp: Select User Where Error.LogonFailure > 3 AND LogonFailure.User AND Duration < 1hour Sorted By date, time
