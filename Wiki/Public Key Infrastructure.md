*PKI is the entire system, which uses public key cryptography to operate*

## Authorities
1. Certificate Authority
2. Verification Authority
3. Registration Authority

![grafik](https://user-images.githubusercontent.com/84674087/132235108-1a3e548a-1dc6-43d2-9810-3d7c1755d77d.png)


## Certificate Content
1. Identification information
2. Public Key
3. Certification Authority
4. Signature of Certification Authority 
5. SAN (Subject Alternative Name):
   - Allows cert owner to specify additional domains/IPv4/6 

## Certificate Types
1. Wildcard Certificates
   - Allow all subdomains to use same public key
   - Easier to manage than normal certificates
   - If public key gets revoked, all subdomains are affected (!)
2. Single-sided Certificates
   - Only the server has to validate itself
3. Dual-sided Certificates
   - Client and Server verify themselves
   - Better security, but requires twice processing power (!)

## Common PKI Issues
- Key Rotation: Keys dont expire (like Certs) -> force regular change
- Outdated Protocols: Use Patch Management
- Key Storage: Use Secure Centralized Vault
- Human Error: Avoid Misconfiguration / Improper handling
- Insufficient Key Length: Brute Force (!)

## Key Management
- Key Escrow: Holds a secure copy of the private key
- Key Recovery Agent: Backup SW for lost/corrupted keys
- CRL (Certificate Revocation List): Online list about all revoked certificates of the respective CA
- CSR (Certificate Signing Request): Send to CA to request a new digital certificate (in case the certificate is about to expire)
- OCSP (Online Certificate Status Protocol): 
    - Alternative to CRL
    - Quicker and more efficient
    - Doesn't use encryption (!)
      - Solution is OCSP Stapling: OCSP + integrated as part of TLS handshake (more secure)
