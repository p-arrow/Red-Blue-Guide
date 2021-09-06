*Alternate Data Streams: Meta data attached to another medium (text, picture etc.)*

## Charakteristic
- Both GUI and CLI don't show ADS by default
- Size of carrier medium is not affected by ADS 
- Can be used to transport stealthy malicious code 
- Only available under Windows

## How To (text file)
1. Create text file: test.txt and fill in arbitrary data, save 
2. Create ADS via CMD: `notepad test.txt:secret.txt`, write arbitrary data into ADS file, save and close
3. CMD: `dir` (to display test.txt)
4. CMD: `dir /r` (to display test.txt and secret.txt)
5. Edit ADS: Enter in CLI `notepad test.txt:secret.txt`
6. Remove ADS: Copy carrier medium on FAT-Volume, because FAT cannot handle ADS
