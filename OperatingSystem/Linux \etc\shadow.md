
## etc/shadow
- **/etc/passwd --> 644 / rw-r--r--**
- **/etc/shadow --> 640 / rw-r-----**

#### Format /etc/shadow
1. User
2. PW-Hash
   -  Hash Algorithm
   -  Salt (in between two $ signs)
   -  PW + Salt Hash
3. last change
4. Min.Days between PW change
5. PW validity
6. Warning threshold
7. Account inactive (days)
8. Time since account is disabled

![grafik](https://user-images.githubusercontent.com/84674087/133145945-6f2abac5-ac9d-41b4-b5a0-a53b14ee0aac.png)

#### Format /etc/passwd

![grafik](https://user-images.githubusercontent.com/84674087/133145975-8aea2c1e-ff8c-4db9-8373-c67905fdbda0.png)

#### Hash-Code /etc/shadow
- $1: MD5
- $2a: Blowfish
- $2y: eksBlowfish
- $5: SHA256
- $6: SHA512 
