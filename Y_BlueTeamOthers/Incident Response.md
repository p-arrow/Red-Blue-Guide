*Incident: Act of violating an explicit or implied security policy*

*NIST Incident Handling Guide 800-61*

## 1. Preparation

*Hardening, writing policies, set up confidential lines of communication, conduct training*

## 2. Detection & Analysis
*Determine if an incident has taken place, triage it and notify relevant stakeholders*

## 3. Containment

*Limit the scope and magnitude of incident*

1. Ensure the safety and security of all personnel
2. Prevent ongoing intrusion by:
   - Isolation: Remove pc from larger environment (least stealthy!)
   - Segmentation: Prevent comm. outside protected segment
   - Consult with senior leadership to choose proper strategy
3. Identify if intrusion is primary or secondary attack
4. Avoid alerting discovery of attacker (avoid "burn the house down")
5. Preserve forensic evidence

## 4. Eradication & Recovery

*Remove the cause of incident and bring the system back to secure state*

1. Reconstruction
   - Restoring a system after sanitization using scripted install-routines
2. Reimaging
   - Resorting a system using an image-backup (bit by bit)
3. Reconstitution
   - Restoring by manual removal, reinstallation and monitoring
4. For Devices w/o Sanitization
   - Analyze procs/NW for malware activity
   - Terminate suspicious processes and securely delete
   - Identify/Disable autostart locations
   - Replace contaminated procs with clean versions
   - Reboot, then analyze of continued malware infection
   - If so, then analyze firmware and USB devices
   - If tests are negative, reintroduce system to productive environment

*The longest and most challenging part of incident response (!):*

1. Patching: scan vulns, patch, scan if everything is up2date
2. Permissions: should be reviewed and reinforced after incident
3. Logging: Ensure that logging after incident will continue
4. System Hardening: Most effective preventative measure

## 5. Post-incident Activity

*Analyze the incident and identify improvements in procedures*

1. Report Writing: clearly mark the intended audience/stakeholder e.g. Executive Summary
2. Incident Summary Report: For non-technical audience
3. Evidence Retention: Time period depends on regulations
