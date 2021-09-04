## Drawbacks of Embedded Systems

1. Only little support for identifying/correcting security issues (!)
2. Typically cannot tolerate reboots/crashes (!)
3. Must have response time within µs (!)


## PLC (Programmable Logic Controller) 

- A computer designed for industrial area
- Can automate and monitor mechanical systems
- PLC firmware can be patched to fix vulns
- Patch maybe once a year (not frequently!)

## SoC (System-on-Chip)

- Integrates funcionality of multiple logical controller
- Very power efficient
- Used within embedded systems

## RTOS (Real-Time Operating System)

- OS that prioritizes deterministic execution of operations for time-critical tasks

## FPGA (Field Programmable Gate Array)

- Processor can be programmed for specific function by customer (i/o manufacturer)

## CAN (Controller Area Network)

- To connect subsystems
- CAN concept originates from 80s/90s
- No security included back these days (!)
- No source addressing / message authen in CAN (!)
