## Cloud Types
1. **Public Cloud**
2. **Private Cloud**
   - More expensive than public cloud
   - Requires more manpower for configuration/monitoring
3. **Community Cloud**
   - When few tenants (5-10) share resources and cost of a cloud service
4. **Hybrid Cloud**
   - Greater complexity (security management)
   - Absence of data redundancy
   - Demonstrating compliance is more difficult
5. **Multi Cloud**
   - When organization uses several public clouds
   - Requires additional due diligence and risk assessment
   - The Opposite is the "Single Cloud" from only one vendor
6. **All-in** 
   - When all systems are run in the cloud

## Technical Terms for Computing
- **Memory Ballooning**: Unused, allocated RAM for one guest used by another
   - Bursting: The action of ballooning
   - Not managed by user in public clouds (but CSP)
   - Managed by user in private clouds (Open Stack)
- **Dedicated Host**: Physical server used only for your instance(s) (better performance)
- **Clustering**: Use of multiple VMs providing same application with failover options
- **Load balancing**: Use of multiple VMs providing same app with rotation among machines
- **Load Testing**: To verify an instance can handle the proposed demand
- **Thick Provisioning**: 
   - Allocates virtual storage at the time of request
   - More expensive
   - More performance
- **Thin Provisioning**:
   - Allocates virtual storage as needed
   - Less expensive
   - Less performance


## Technical Terms for Storage
- **Synchronous Replication**: at time of data modification
- **Asynchronous Replication**: at scheduled time
- **Cloning**: creates point-in-time copy
- **Mirroring**: creates continuous copy
- **Tokenization**:
   - Token is stored in place of data
   - Token is used to retrieve actual data from secure storage (PII, PHI)
- **Same-Region Replication (SRR)**: Within a region
- **Cross-Region Replication (CRR)**: Across regions
- **Zoning**: Provides access to storage by specific device (often @SAN)

## Cloud Security Threats
1. **Insecure API**
    - Always over HTTPS !
    - Always with service-side input validation!
    - Implement rate-limiting to prevent DoS
2. **Improper Key Management**
   - Use secure authentication and authorization
   - Do not hardcode or embed a key in your source code
   - Delete unnecessary keys
3. **Insufficient Logging and Monitoring**
   - SaaS may not supply access to log files
4. **Unprotected Storage**
   - Consider access control to storage via policies/IAM/object ACLs
   - Change default read/write permissions leftover from creation
   - Incorrect origin settings may occur when using CDN:
   - CORS (Cross Origin Resource Sharing): 
     - Instructs browser to treat requests from nominated domains as safe
     - Weak CORS policies expose your site to XSS
5. **VM sprawl/dormant VMs**
   - VM that is created and configured for particular purpose
   - Afterwards shut down/left running w/o properly decommissioning it (!)

## Security Questions
1. **SaaS**
   - Who has access? (IAM)
   - What can they do? (Authorization)
2. **PaaS**
   - Who has access to test/run/deploy code? (IAM / Data encryption)
   - Who can run the code? (Authorization / Load balancing)
3. **IaaS**
   - Who has access to cloud management? (IAM)
   - Who has access to develop?
   - Who has access to run the applications?

<br />

![grafik](https://user-images.githubusercontent.com/84674087/140798329-6ef4585d-cbd8-45b6-9238-6312bebe3b42.png)
