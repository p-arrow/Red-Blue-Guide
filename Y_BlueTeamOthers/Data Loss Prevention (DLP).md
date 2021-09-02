## Types
1. Endpoint DLP System: Software-based client on PC (in use)
2. Network DLP System: Installed at network (in transit)
3. Storage DLP System: Software installed on file servers (at rest)
4. Cloud DLP System: SaaS

### Encryption at Rest

**1) File Level Encryption**
- Lowest level of security
- Encryption of Data files

**2) Directory Level Encryption**
- Works as container for several sensitive files
- Encryption of Data files

**3) Full Disk Encryption (FDE)**
- Highest level of security
- Encryption of System files + Data files

**Linux Tools for Encryption at Rest**
- GPG
- ccrypt
- 7-zip


**FDE**

![grafik](https://user-images.githubusercontent.com/84674087/131902185-1e3a7742-4a72-4194-8a64-3703400074a3.png)



## DLP Functions
- Alert only
- Block
- Quarantine: Encrypt the regarded file
- Tombstone: Origin file is not only quarantined but also replaced (to prevent DL again)


## How Protected Data is marked
- Classification: Based on tags/labels attached to data
- Dictionary: Set of patterns that should be matched
- Policy Template: Optimized dictionary for data points in a regulatory scheme
- Exact Data Match (EDM): Structured database with hashes
- Document Matching: Based on entire/partial document hash
- Statistical/Lexicon: Refinement of partial doc matching with Machine Learning
