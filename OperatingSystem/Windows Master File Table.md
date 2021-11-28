## Characteristic
- Each file on NTFS has record in master file table
- NTFS reserves first 16 records of the table for special information
- First record describes MFT itself, followed by MFT mirror record
- If first MFT record is corrupted, MFT mirror can be used
- Small Files/Directories: <512 Bytes
- Small Records can entirely be contained in MFT

#### NTFS performs faster Data Access compared to FAT (File Allocation Table), because ...
- FAT first reads the file allocation table and assures that it exists
- FAT retrieves the file by searching the chain of allocation units assigned to the file
- With NTFS, as soon as you look up file, it's there to use

<br />

![grafik](https://user-images.githubusercontent.com/84674087/140794801-936f790a-ad9e-4706-9299-e372dd7c8c70.png)
