*Disposal of obsolete information/equipment (part of IR Eradication)*


## Cryptographic Erase (SSD/HDD)
- Used for storage media that is encrypted by default
- The encryption key itself is destroyed during the erasing operation

## Zero-fill (HDD)
- Overwriting all bits to Zero
- CMD: `format c: /fs:NTFS /p:1`
   - /p:1 = one set of zeros over c
- Zero-Fill is not sufficient for SSD's (!)
- Because device uses wear-leveling routines in the drive controller (!)
- To communicate which locations are available for use to any SW process accessing the device (!)

## Data Wiping
- 1x, 7x, or 35x overwriting
- The higher the number of times, the more secure

## Degausser (HDD)
- Demagnetizing a hard drive to erase its stored data
- Reuse of disk impossible (!)

## Shredding
- Physical destruction of disk

## Purging
- Removing sensitive data by using the device's own electronics
- Reuse of disk impossible (!)
