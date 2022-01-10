# Blue Team

*What you know/are/have/do/and where you are*

## Types

#### 1) Context-aware Authentication
- Check user's/system's attributes or characteristic
- Prior login

#### 2) SSO (Single Sign-On)
- One complex PW but access to all ressources (efficient)
- Cryptography hash of credentials is passed between systems

#### 3) FIdM (Federated Identity Management)
- Single Identity for one user
- Shared with all organizations in a federation
- Based on Cross-Certification (Web of Trust): Good for small NW
- Based on Trusted Third-Party: Good for big NW
- Example: 
    - a) SAML (Security Assertion Markup Language)
    - b) OpenID:
       - OpenID easier to implement than SAML (but less efficient)
       - Sign-on provided as service by ID provider (google, fb) 
       - Automatic Provisioning, when log-on to Service Provider (SP)
       - PW loss/change has to be addressed to ID provider (i/o SP)

#### 4) HSM (Hardware Security Module)
- Physical device that safeguards digital keys
- Encryption/Decryption of digital signature (strong authentication)
- Super Secure Password Storage: PW + Salt + Hash + 1000xIteration + Encryption + HSM

#### 5) HMAC (hash-based Message Authentication Code)
- No encryption of messages 
- Used for Integrity and Authentication
- Used in IPSec, SSH, TLS

#### 6) OTP (One Time Password)
- User needs to type codes during login process
- Can be single point of attack (Background Server stores data) (!)
- Phishing Attack/MITM is possible (Attackers uses fake website to obtain credentials) (!)

#### 7) U2F (Universal 2nd Factor)
- Kind of successor of OTP
- Based on public key cryptography
- Challenge from legitimate server, Response from browser
- No codes to re-type
- Supported by Chrome only, Firefox might follow

#### 8) FIDO (Fast IDentity Online)
- (+) Similar to 2FA, but w/o entering code from another device
- (+) more comfort (w/o relying on PWs)
- (+) more secure (Token = PC/phone/Yubikey)
- (-) could be stolen
- (-) not always kept in pocket
- (-) more expensive
- (-) not widely used yet
- (-) not all PCs have USB C or NFC support (for Yubikey)

#### 9) LDAP (L7)
- Active Directory (Windows) uses LDAP
