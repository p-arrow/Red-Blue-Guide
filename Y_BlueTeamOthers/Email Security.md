## Infrastructure

**MTA (Mail Transfer Agent)**
- Mailserver
- Exp: exim, sendmail

**MDA (Mail Delivery Agent)**
- Sorts receving mails
- Exp: procmail

**MUA (Mail User Agent)**
- Mailclient of User
- Storage: /var/mail/[user]
- Exp: mutt

**All-rounder (MUA+MDA+MTA)**
- GNOME Evolution
- KDE kmail
- Thunderbird

## Attack Vectors

1. BEC (Business Email Compromise): Impersonation attacks
2. Forwarding: Formatted Phishing mail appears as reply
3. Email Header Analysis: Record of email servers involved
   - MUA-> MDA-> MTA-> MTA-> MDA-> MUA
4. Attackers obfuscate: Display / Envelope / Received from
5. Flash/Java/JS: Web-Attacks (Webmail) ; HTML/CSS can be malicious
6. Cousin Domain: Attacker copy setup of DMARC / DKIM / SPF
    - Then Recipient MTA will accept this Cousin Domain

## Best Practice (Corporation)

**SPF (Sender Policy Framework)**
- Only authorized hosts of a domain are allowed to send mails
- These hosts are listed in DNS record, which email server cross-check

**DKIM (DomainKeys Identified Mail)**
- Cryptographic mail authentication by using public key published as DNS record
- It's like digital signature but done by email serves (i/o email clients)

**DANE (DNS-based Authentication of Named Entities)**
- An additional test procedure to enhance TLS and avoid MitM attacks
- It confirms that your counterpart is really your counterpart based on certificate verification (TLS-Authentication Record)
- Utilizes  DNSSEC (Domain Name System Security Extensions)

**OpenPGP**
- Common Standard for email encryption
- Best Practices: [riseup.net/OpenPGP](https://riseup.net/en/security/message-security/openpgp/best-practices#use-the-sks-keyserver-pool-instead-of-one-specific-server-with-secure-connections)


**DMARC (Domain-Based Message Authentication, Reporting and Conformance)**
- Framework for ensuring proper application of SPF and DKIM
- Based on policy published as DNS record

![grafik](https://user-images.githubusercontent.com/84674087/131900599-a4ae7b95-3566-4c25-a7c3-8a3acfe15617.png)

## Best Practice (Individual)

1. Use mail providers that encrypt email transfer (server2server connections)
2. Use encryption for the communication between your email client and email server: IMAP Port 993 / POP3 Port 995 ; SMTP Port 465 (STARTTLS Port 587)
3. Use email encryption (OpenPGP, S/MIME)
4. Encrypt your email account / email archive (data at rest)
