## Table of Content
- [[Configure the arch system#Make Your Partition persistent|Make Your Partition persistence]]
-  [[Configure the arch system#Chroot|Chroot]]
- [[Configure the arch system#Basic configuration|Basic Configuration]] optional but recommended
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

### Chroot
Change root system from live boot to main partition new system [[Arch]] gonna install. 
to use [[Chroot]]
> [!info] 
> some systemd tool not run in chroot like `hostnamectl`, `timedatectl`, `localectl` . it's required [[dbus]] connection

```bash
arch-chroot /mnt
```
now live boot terminal change it's root to mount partition root



### Basic configuration 
after using [[Chroot]] you basically use root in main OS not live boot,
means whatever configuration you do it's directly effect the main arch O.S 
as you boot into main O.S that done in advance 
but it's optional right now 
to configure like 
- [Time](https://wiki.archlinux.org/title/Installation_guide#:~:text=For%20human%20convenience%20(e.g.%20showing%20the%20correct%20local%20time%20or%20handling%20Daylight%20Saving%20Time)%2C%20set%20the%20time%20zone%3A)
- [Localization](https://wiki.archlinux.org/title/Installation_guide#:~:text=To%20use%20the,locales%20by%20running%3A)
- [Network configuration](To assign a consistent, identifiable name to your system (particularly useful in a networked environment), [create](https://wiki.archlinux.org/title/Create "Create") the [hostname](https://wiki.archlinux.org/title/Hostname "Hostname") file)

> [!info] 
> These configuration is optional right now we can do it letter in [[Post arch installtion]]

**Next Step**
[[Arch Boot loader setup]]


### See also
[refrence](https://wiki.archlinux.org/title/D-Bus#:~:text=is%20a%20message%20bus%20system%20that%20provides%20an%20easy%20way%20for%20inter%2Dprocess%20communication.%20It%20consists%20of%20a%20daemon%2C%20which%20can%20be%20run%20both%20system%2Dwide%20and%20for%20each%20user%20session%2C%20and%20a%20set%20of%20libraries%20to%20allow%20applications%20to%20use%20D%2DBus.)