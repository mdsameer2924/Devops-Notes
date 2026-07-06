**Related to :** { [[Arch]] , [[Operating system]] }
## Table of Content
- [[Arch Boot loader setup#Choose a Boot loader|Choose Boot loader]]
- [[Arch Boot loader setup#Setup Boot loader|Setup Boot loader]]
- [[Arch Boot loader setup#Troubleshoot Problem|Troubleshoot  Problem]]

**prerequisites**
1. [[Arch linux partition#mount partition|Mount partition]] to get access of partition in live boot
2. [[Configure the arch system#Chroot|Chroot]] to change root new system 
3.  All operation done further in main system linux now live boot 
4. Change root password of that system `passwd root`


### Choose a Boot loader 
even if operating system installed in system but [[Boot loader]] is a piece of code which boot Operating system into System,
without boot loader fully fledged Operating system trash unable to use  
> I choose grub

first install the bootloader and [[efibootmgr]] 
```bash
pacman -S grub
pacman -S efibootmgr
```
install `os-prober` as well to detect other operating system as well
```bash
pacman -S os-prober
```
### Setup Boot loader
boot loader setup 
**Target directory :** `/boot/efi`   
**Target Partition**:  EFI partition, in my case `/dev/sda2`
**Typical size of EFI partition :** 1GIB  
**file system :** `FAT32`

before setup ensure  in `/boot` directory our **efi directory is exist**
then mount 
```bash
mkdir -p /boot/efi  #creat efi dir
mount /dev/sda2 /boot/efi
```

to check the status work or not use `lsblk`
```bash
[root@archiso /]# mount /dev/sda2 /boot/efi
[root@archiso /]# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0  986M  1 loop 
sda      8:0    0 42.2G  0 disk 
├─sda1   8:1    0   35G  0 part /
├─sda2   8:2    0    1G  0 part /boot/efi
└─sda3   8:3    0  4.5G  0 part 
sr0     11:0    1  1.5G  1 rom  
sr1     11:1    1  1.5G  1 rom  
```

now as you see, in `sda2` partition **MOUNTPOINTS** set as `/boot/efi`
means works 

**Now it's time to install grub boot loader into system**
```bash
 grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB
```
command broke to understand:
`grub-install` -- to install grub bootloacer
`--target=x86_68-efi` -- set architecture install 64 bit
`--efi-directory=/boot/efi` --> to tell the installed in this directory
`--bootloader-id=GRUB` --> set the id in system it's shows and label as GRUB

after this grub must be install in EFI Partition but might be throw error just like my case 
it's throw 
```bash
Installing for x86_64-efi platform.
EFI variables are not supported on this system.
EFI variables are not supported on this system.
grub-install: error: efibootmgr failed to register the boot entry: No such file or directory.
```

### POST Boot loader installation

now after installed bootloader into EFI partition then make a config file 
```bash
grub-mkconfig -o /boot/grub/grub.cfg   
```
add it's make a **`grub.cfg`** file which scan and let bootloader to boot operation system

then, 
exit the `chroot` and `Unmount` all mount partition into live boot 
```bash
exit #to exit chroot
umount -R /mnt #unmount all partition root and efi
reboot
```

### IF still arch not bootinto main system make sure there file directory exact like
```bash
└── boot/
    ├── vmlinuz-linux              <-- The actual Linux Kernel
    ├── initramfs-linux.img        <-- The initial RAM disk (drivers loaded before root)
    │
    ├── efi/                       <-- Mount point for your EFI Partition (/dev/sda2)
    │   └── efi/
    │       ├── BOOT/
    │       │   └── BOOTX64.EFI    <-- Default fallback UEFI bootloader
    │       └── GRUB/
    │           └── grubx64.efi    <-- The actual GRUB binary executed by your motherboard
    │
    └── grub/                      <-- GRUB configuration and assets directory
        ├── grub.cfg               <-- THE MAIN CONFIG FILE (what was empty before)
        ├── grubenv                <-- GRUB environment variables storage
        ├── x86_64-efi/            <-- Internal GRUB modules (.mod files) for filesystems/features
        └── themes/
            └── starfield/         <-- Visual assets, fonts, and images for the boot menu
```
### Troubleshoot Problem 
start with Why ?
	error occur because  I am using **Legacy BOIS** but `efibootmgr` is **UEFI compatible**.
to fix i have to 
![[Pasted image 20260704184132.png]]
enable UEFI in vm box as  in image shows
and after this tried again then  work 

**problem fix**
![[Pasted image 20260704183344.png]]
#### see also
[refer](https://wiki.archlinux.org/title/Arch_boot_process#Boot_loader)
[user-freindly](https://arch.d3sox.me/installation/)
