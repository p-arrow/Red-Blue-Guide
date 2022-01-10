# Blue Team

<br />

## Characteristic
- less efficient than symmetric cryptography 
- more complex way of operation 
- longer key length than symmetric cryptography
- mainly used for authentication and key exchange 

## Algorithms

#### Diffie-Hellmann (DH)
- First asymmetric algorithm from 1976
- Mainly used for IPSec and SSH 

#### RSA Algorithmus 1977
- Uses big prime numbers and hash functions starting from 512 Bit 
- General recommendtaion: 2048 Bit (or longer) key length
- Used for key exchange and authentication 

#### Elgamal 1984
- Similar to DH
- Used for Encryption and Signature 

#### Digital Signature Algorithm (DSA)
- Based on Elgamal 
- Invented by NSA

#### ECC (Elliptic Curve Cryptography)
- ECC 256bit key is as secure as RSA 2048bit key (efficient!)
- Therefore often used in mobile devices
- Variations: ECDH, ECDHE, ECDSA

#### One-Time Pad
- The only truly unbreakable encryption, but requires two identical pads
- Generally, computer cannot calculate truly random numbers
- Instead, they use PRNG (Pseudo-Random Number Generator)
- PRNG used in cryptography, video games etc.
