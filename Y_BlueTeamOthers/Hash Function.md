## Properties
- Unkeyed Cryptographic Primitives
- One way function
- Variable Input length - Fixed Output length
- Very efficient (fast calculation)
- **Target: To ensure lowest possible chance for collision**

*Fast Hash: MD5, SHA1, SHA256*

*Slow Hash: bcrypt, scrypt*


## Hash Algorithms

#### Message Digest 5 (MD5)
- From 1991
- 128Bit Hash
- Not secure anymore!

#### Secure Hash Algorithm (SHA-1)
- From 1995
- Developed by NIST/NSA
- 160 Bit (not secure anymore!)
- Recommended: SHA-2 (256 Bit) / SHA-3 (384 Bit)

#### Password-Based Key Derivation Function 2 (PBKDF2)
- Optimized PW storing (exp: WPA/WPA2)
- (Weakness: Easy to implement in HW)

#### Bcrypt(1999) and Scrypt(2010)
- Optimized PW storing
- Based on Blowfish
- (More resistent against HW implementation compared to PBKDF2)

#### LM Hash (LAN Manager Hash)
- Always 14 characters long (shorter PW is filled up with zeros)
- All characters are turned into uppercase letters before encoding 
- 14 char PW is separated into teo 7 char PWs (!)
- Encryption is based on DES (!)
- LM Hashes are deactivated since Windows Vista by default

#### NTLM Hash (NT LAN Manager Hash)
- Released with Windows NT 3.1 in 1993
- NTLM uses RC4-HMAC algorithm
- 128 Bit output
- Management via SAM (windows/system32/config/SAM)

#### NTLMv2
- Uses HMAC-MD5
- Used when domain operates without Kerberos authentication or when no domain is in place

#### RIPEMD (RACE Integrity Primitive Evaluation Message Digest)
- Open source hash algorithm
- Creates 160bit (most common), 256bit and 320bit message digests
