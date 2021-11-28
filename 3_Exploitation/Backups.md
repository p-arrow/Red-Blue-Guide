# Blue Team

<br />

## 1. Full Backup
- Complete backup but time consuming and costly

## 2. Differential Backup
- Takes more time to create but less time to restore
- Only backups data since the last full backup

## 3. Incremental Backup
- Takes less time to create but more time to restore
- Backsup only data changed since last backup

## 4. Snapshots
- Very handy but use a lot of space!


## Differential vs Incremental (after Failure)

![grafik](https://user-images.githubusercontent.com/84674087/131898234-23a3a52e-9609-4721-b141-12944d56232d.png)

## Tape Rotation

**1. 10 Tape Rotation**
- Each tape used once per day for two weeks
- Then entire set reused

**2. Grandfather-Father-Son (GFS)**
- Son (Daily)
- Father (weekly)
- Grandfather (monthly)

**3. Towers of Hanoi**
- Like GFS but more complex

**4. 3-2-1 Rule**

![grafik](https://user-images.githubusercontent.com/84674087/132099357-afbdcabb-8331-4400-9d7c-cd314c136d30.png)
