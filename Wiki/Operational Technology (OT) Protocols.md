*Operational Technology prioritize availability and integrity over confidentiality (!)*

## ICS (Industrial Control Systems)
- A NW that manages embedded devices
- Uses Fieldbus to link PLCs within an OT network
- HMI (Human Machine Interface) on a PLC
- Data Historian: Software that aggregates/catalogs data within ICS

## SCADA (Supervisory Control and Data Acquisition)
- Type of ICS that manages large-scale multiple-site devices

## Modbus
- Communication protocol used in OT network (proprietary)
- It's alike TCP, but for OT
- Provides ability to query and change configs of each PLC

## Best Practice
- NIST-82: Guide to Industrial Control Systems
   - Establish administrative control over OT
   - Implement minimum network links (disable services/protocols )
   - Develop/Test patch management for OT networks
   - Perform regular audits
- Vuln scanners can cause problems to OT NWs (!)
- Better: Passive Analysis
