## Prefetch file
- Stores data when application starts (date/time, DLLs, file path)
- Disabled by default on Windows Server platforms?!

## Shimcache (application compatibility cache)
- Created by Microsoft (Win XP) to track compatibility issues
- Helps troubleshoot legacy functions 
- Tracks metadata: full file path, last modified date, file size
- Current entries are stored only in Memory
- Only written to Registry when system is shutdown
   - Volatility Framework for LiveParsing!
- New Entries created when file’s metadata changed + re-executed
- `HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\AppCompactCache`

## Amcache
- What: Application Usage Cache stored as hive file
- Where: `C:\WINDOWS\appcompat\Programs\Amcache.hve`
- About: execution path, first executed / deleted time, first installation
- Was called "RecentFileCache.bcf" (before Win7)
