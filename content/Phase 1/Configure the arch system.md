## Table of Content
- [[Configure the arch system#Make Your Partition persistent|Make Your Partition persistence]]
- 
### Make  Your Partition persistent 
as you earlier  [[Arch linux partition#mount partition|mount]]  partition using `mount` as a temporary to make it persistence
enter partition entries into `/etc/fstab`

```bash
genfstab -U /mnt /mnt/etc/fstab
```

because of liveboot arch  `/mnt/etc/fstab`
because i give /mnt -> `/`
and `/mnt/boot` -> **EFI partition**

**for example**
**Before** `/etc/fstab` entries
```bash
[root@archiso /]# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0  986M  1 loop 
sda      8:0    0 42.2G  0 disk 
├─sda1   8:1    0   35G  0 part /mnt
├─sda2   8:2    0    1G  0 part /mnt/boot
└─sda3   8:3    0  4.5G  0 part [SWAP]
sr0     11:0    1  1.5G  1 rom  
sr1     11:1    1  1.5G  1 rom 
```

**After** `/etc/fstab` entries
```bash
[root@archiso /]# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0  986M  1 loop 
sda      8:0    0 42.2G  0 disk 
├─sda1   8:1    0   35G  0 part /
├─sda2   8:2    0    1G  0 part /boot
└─sda3   8:3    0  4.5G  0 part [SWAP]
sr0     11:0    1  1.5G  1 rom  
sr1     11:1    1  1.5G  1 rom 
```

### 