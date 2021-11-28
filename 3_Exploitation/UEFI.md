# Blue Team

<br />

## Secure Boot
- Digital certificates from valid OS vendor are cross-checked

## Measured Boot
- Gathers secure metrics to validate and attest it in a report

## Attestation
- Claim valid report data by digitally signing via TPM's private key

## eFUSE
- Permanently alter the state of a transistor on a computer chip
- Emergency solution in case of compromise

## Trusted Firmware Updates
- Signed by vendor
- Thus trusted by system (otherwise eFUSE reacts)

## Self-Encrypting Drives
- Incl. firmware controller that can automatically encrypt/decrypt
