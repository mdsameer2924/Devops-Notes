package mirror list with download url stored into 
**Path**: `/etc/pacman.d/mirrorlist` we can inspect these package mirror list 
and edit according or leave it default 

then,  in this `mirrorlist` contain priority based package which is only enough to boot Linux in our  system letter we install manually other package,

to installs after check all the mirrorlist, 
use [[pacstrap]] script to install all of these base package,
which it's process from 
-  `/etc/pacman.d/mirrorlist` : all crucial package mirror link use to installed package
-  `/etc/pacman.d/gnupg`: verify package using gpg keyring 

```bash
pacstrap -K /mnt base linux linux-firmware
```
**What it does install ?**
- installed all drivers file like , wifi, bluetooth
- installed [[Systemd]] 1st process  
- install and assign [[User and group|group]] and it's ID
and too many base package installed which is very crucial for booting system

**Next Step**
[[Configure the arch system|Configure the system]]