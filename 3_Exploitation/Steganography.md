Check out: [https://book.hacktricks.xyz/stego/stego-tricks](https://book.hacktricks.xyz/stego/stego-tricks)

# RedTeam

## Stego/Forensic Tools

#### General
- Binwalk
- Foremost
- Exiftool
- Bulk extractor
- File
- Strings
     - `strings -n 6 [file]` show only strings with min length of 6 chars 
- cmp
- Steghide
     - `steghide info file`
     - `steghide extract -sf file` 
- Magic rescue: "This tool uses magic bytes to extract all the known file types from the device"

#### Images
- Zsteg: [https://github.com/zed-0xff/zsteg](https://github.com/zed-0xff/zsteg)


#### Audio

- ffmpeg
- Wavsteg --> [https://github.com/ragibson/Steganography#WavSteg](https://github.com/ragibson/Steganography#WavSteg)
- Sonic Visualizer: [https://www.sonicvisualiser.org/](https://www.sonicvisualiser.org/)
    - "Sonic Visualiser is a free, open-source application for Windows, Linux, and Mac, designed to [...] to study a music recording closely"

#### Pdf
- pdfid
- pdf-parser
