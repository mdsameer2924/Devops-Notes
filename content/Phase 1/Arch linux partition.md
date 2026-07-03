
## Table of Content
- [[Arch linux partition#format for Arch|Format for Arch]]
- [[Arch linux partition#mount partition|mount partition]]
----
now create three partitions
**/** -  root  size must be 20-more 
/boot - at least 1GiB
/swap -  at least 4 GiB

for partition process [[how to create parition in linux|click here ]]

### format for Arch 


1. / partition can be `ext4` or `xfs`
```bash
mkfs.ext4 /dev/sda1 # root directory
```

2. /boot partition is universal file system which is fat32 to stores UEFI's boot file it can store multiple O.S bootloader file at once which later read by nvram through firmware
```bash
mkfs.fat -F 32 /dev/sda2 # boot efi partition
```

3.  /swap this partition is optional best best for prepare for broken system or ram full then stays here inactive data here work as a [[virutal memory]]
```bash
mkswap /dev/sda3 # swap partition 

```




### mount partition 
1. **root partition**: 
```bash
mount /dev/sda1 /mnt # temp mount
```
2. **boot partition**:
```bash
mkdir -p /mnt/boot ## create EFI dir
mount /dev/sda2 /mnt/boot
```
3. **swap partition**:
```bash
swapon -v /dev/sda3 # just on swap for pagging
```

file result after this:
![[Pasted image 20260702202016.png]]

**Next Step** 
[[Installation crucial package]]












### See also 
[reference ](https://wiki.archlinux.org/title/Installation_guide#:~:text=installing%20the%20system.-,Example%20layouts,-UEFI%20with%20GPT)
