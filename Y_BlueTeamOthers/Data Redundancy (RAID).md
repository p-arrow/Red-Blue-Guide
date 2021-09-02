## Categories
1. Fault-resistant (Raid1/5)
2. Fault-tolerant (Raid1/5/6)
3. Disaster-tolerant (Raid10)


## 2 disks, performance increase (shared load/striping)

![grafik](https://user-images.githubusercontent.com/84674087/131898377-db1b1c48-2dd9-47d9-8411-abce1019dd46.png)


## 2 disks, redundancy increase (mirroring)

![grafik](https://user-images.githubusercontent.com/84674087/131898402-e4940737-b649-4f81-8d9d-7cc7028fb76e.png)


## 3 disks, redundancy increase (rebuild itself if 1xdisk is lost)

*Parity Bit is rotating through all disks*

![grafik](https://user-images.githubusercontent.com/84674087/131898424-7aafe703-1593-4ac9-ab25-3bcfdebaefe8.png)


## 4 disks, redundancy increase (rebuild itself if 2xdisks are lost)

*Parity + Q Bit is rotating through all disks*

![grafik](https://user-images.githubusercontent.com/84674087/131898444-4f9e58c7-0756-4bbe-b989-4e3dd431bf4f.png)


## Raid 10: 4 disks, Raid 0 + Raid 1 combined

![grafik](https://user-images.githubusercontent.com/84674087/131898464-a20c1bf0-cdb4-483e-9622-7913bbe837e5.png)
