*Private Key Cryptography*

## Basics

### Features/Advantages
- Efficient (100-1000x faster than asymmetric cryptography)
- Short(er) key length
- Good for big data 

### Stream Cipher
- Bit by bit encryption 
- Good for real time application (video, audio)
- Often used for hardware solutions

### Block Cipher (DES, 3DES, AES)
- Easier to implement (than Stream Cipher)
- Less susceptible to security problems
- Often used for software solutions

### Initialization Vector (IV)
- Block of bits that is used by several modes
- To randomize encryption and to produce distinct ciphertexts
- Even if the same plaintext is encrypted multiple times

### Synthetic IV (SIV)
- Pseudo-Random Function (called S2V) + Input (additional data and plaintext)
- Preventing any external data from directly controlling the IV
- External IV may be feed into S2V as additional data field
- Bsp: AES-GCM-SIV

### Modes of Operation

*Cipher Suite encrypts/decrypts only one code block*

*Modes repeatedly apply this on several blocks!*

*For Confidentiality! Not Integrity*

#### a) ECB (Electronic Code Book), from 1981

- simpelst mode (!)
- message is divided into blocks, each block is encrypted separately
- encrypts identical plaintext blocks into identical ciphertext blocks
- lack of diffusion, does not hide data patterns

#### b) CFB (Cipher Feedback), from 1981

- encryption is sequential (no parallelization) (!)
- decryption can be parallelized

#### c) CBC (Cipher Block Chaining), from 1981

- each block of plaintext is XORed with previous ciphertext block before being encrypted
- each ciphertext block depends on all plaintext blocks processed up to that point (chaining)
- most commonly used mode of operation
- encryption is sequential (no parallelization) (!)
- decryption can be parallelized

#### d) OFB (Output Feedback), from 1981

#### e) CTR (Counter), from 2001

#### f) XTS-AES, from 2010

#### g) CTS (Ciphertext Stealing): not officially approved by NIST


### For Integrity

- HMAC (2002)
- CMAC (2005)
- GMAC (2007): Galois/Counter MAC
- Poly1305

### Authenticated Encryption

*Confidentiality and Integrity combined*

- CCM (Counter with CBC-MAC)
- GCM (Galois Counter Mode)
- CWC
- OAB 

## Symmetric Cryptography Algorithms

#### DES (Data Encryption Standard)
- Block Cypher 64 Bit (56 Bit)
- Published in 1977

#### 3DES/DESede
- 168 Bit (112 Bit)

#### AES (Advanced Encryption Standard)
- Block Cypher 128/192/256 Bit
- Published in year 2000

#### Blowfish und Twofish
- From Bruce Schneier(among 5 AES Finalists 2000)

#### Serpent
- Safest but slowest algorithmus (among 5 AES Finalists 2000)

#### IDEA (International Data Encryption Algorithm)
- Symmetric block cipher
- Used inside PGP
- 64bit blocks used
- 128bit key

#### RC4 (Rivest Cipher)
- RC1/2/3 never succeeded
- Symmetric stream cipher
- Variable key from 40 - 2048 bits
- Used in SSL and WEP

#### RC5
- Block Cipher
- Key up to 2048 bits

#### RC6
- Based on RC5
- Block Cipher
- Designed as replacement for DES

#### PGP (Pretty Good Privacy)
- Uses IDEA

#### GPG (GNU Privacy Guard)
- Newer and updated version of PGP
- Uses AES
- Cross-platform availablity
