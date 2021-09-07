*Windows*

## Characteristic
1. Manages the **Unique Sequence Number (USN)** change journal
2. One journal for one disc volume
3. USN Change Journal provides persistent log of all file changes on volume
4. As files/dirs are modified, NTFS enters records into the USN Change Journal
5. Each record indicates the type of change and the object changed
6. New records are appended to the end of stream

## CMD
```
fsutil usn readjournal C: <option>
fsutil file queryFileNameById C:\ "0x" + <Data-ID>
```
