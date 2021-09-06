*Extracting data from computer when that data has no associated file system metadata*

## Background
- HDD and SSD are divided into sectors
- 512 bytes (standard) or 4096 bytes (Advanced)
- Block is smallest unit a file system can address (default 4096 bytes)
- Thus big files are broken into sector-friendly pieces and stored

## MFT (Master File Table)
- Contains metadata with location of each file
- When deleting a file you delete the metadata/entry of this file
- But the file still exists!
- These files are marked as "free space", and could be overwritten
- When you need to recover deleted files: Stop using the computer to minimize overwriting risk
