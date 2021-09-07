## Forensic Work Cycle
1. Identification: Ensure safe scene & prevent evidence contamination
2. Collection: Ensure authorization to collect evidence
3. Analysis: Create copy of evidence, i.e. original -> image -> copy
4. Reporting: About methods, tools used and conclusions

**> Every step must follow written procedures (!)**

## Forensic Ethics
- Analysis must be performed without bias
- Analysis methods must be repeatable by third parties
- Evidence must not be changed/manipulated

**> Some attorneys use any deviation of ethics to dismiss your analysis (!)**

## Chain of Custody
- Record of evidence from collection to presentation in court
- Specialized evidence bags are used for electronic media
- Properly label all evidence

## Data Collection Procedures
1. Create forensic disk image of data (for law enforcement)
2. "Chain of custody" to document collection&preservation
3. Track man-hours and expenses
4. Capture evidence in the following order:
   1. CPU registers
   2. Cache
   3. RAM
   4. Routing table
   5. ARP
   6. Kernel
   7. Swap
   8. SSD
   9. HDD
   10. Screenshots/Videos

## Work Product Retention
- Attorney hires forensic analyst (two party contract), not the victim!
- Attorney decides if analysis can be disclosed to def./prosecution

## Forensic Workstations
- Must have multiple cores
- Lot of RAM (>64GB)
- Lot of SSD space or SAN
- Multi media reader (CD,DVD,Blueray,USB,SD Card etc)
- Is prohibited from accessing the internet (!)

## Forensic Tools
- EnCase: proprietary
- FTK (Forensic Toolkit): proprietary
- The Sleuth Kit: open-source
- Timeline: Shows sequence of file system events of image (GUI)
- Memdump
- dd (disc duplicate)
- Forensic Drive Duplicator: Copies drive and validates it matches the original drive
- Hardware Write Blocker: Ensure that Forensic Tools cannot change HDD/SSD
- Software Write Blocker
