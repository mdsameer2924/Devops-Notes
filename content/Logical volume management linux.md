**Related :** { [[Linux]] , [[Disk Management]] }
logical volume management is a way of creating or increase the storage size using logical volume instead limit by block it's work flexible, and can be increase storage size with zero downtime

first have multiple partition
to, check we use lsblk
```bash
nvme0n1      259:0    0    8G  0 disk 
├─nvme0n1p1  259:1    0  6.9G  0 part /
├─nvme0n1p13 259:2    0 1023M  0 part /boot
├─nvme0n1p14 259:3    0    4M  0 part 
└─nvme0n1p15 259:4    0  106M  0 part /boot/efi
nvme1n1      259:5    0   10G  0 disk 
nvme2n1      259:6    0   12G  0 disk 
nvme3n1      259:7    0   14G  0 disk 

```

then use `lvm` command but before use it switch into normal user to **root** use 
`sudo su`, then type `lvm`

```bash
root@ip-172-31-15-156:/home/ubuntu# lvm
lvm>
``` 

as you type lvm it's look like this, 
then create 
before create any logical volume we known about some basic theory
> [!info] `physical volume` se banta hain `Volume group` and usse banta hain `logical volume`

now right these disk is just normal disk not **physical volume** 
```
nvme1n1      259:5    0   10G  0 disk 
nvme2n1      259:6    0   12G  0 disk 
nvme3n1      259:7    0   14G  0 disk 
```

### physical volume

```bash
lvm 
lvm> pvcreate /dev/nvme1n1 /dev/nvme2n1 /dev/nvme3n1 
```
now your logical volume successfully created to check use **`pvs`**
also can use 
```bash
lvm> pvdisplay ## just type pvdisplay show in full detail
  --- Physical volume ---
  PV Name               /dev/nvme1n1
  VG Name               sameer
  PV Size               10.00 GiB / not usable 4.00 MiB
  Allocatable           yes 
  PE Size               4.00 MiB
  Total PE              2559
  Free PE               2559
  Allocated PE          0
  PV UUID               oIzQ2q-3y6U-b2CL-SVxN-RZYN-kGdY-uG2uVk
   
  --- Physical volume ---
  PV Name               /dev/nvme2n1
  VG Name               sameer
  PV Size               12.00 GiB / not usable 4.00 MiB
  Allocatable           yes 
  PE Size               4.00 MiB
  Total PE              3071
  Free PE               3071
  Allocated PE          0
  PV UUID               i8XdwB-nsAx-BCLC-ZmDr-PS9j-YpRn-KL0siF
   
  "/dev/nvme3n1" is a new physical volume of "14.00 GiB"
  --- NEW Physical volume ---
  PV Name               /dev/nvme3n1
  VG Name               
  PV Size               14.00 GiB
  Allocatable           NO
  PE Size               0   
  Total PE              0
  Free PE               0
  Allocated PE          0
  PV UUID               DFBCGw-n6Ji-vZ8w-F307-XYOl-IQW1-WW25nt

```
### Volume Group
```bash
lvm
lvm> vgcreate nameofgroup /dev/nvme1n1 /dev/nvme2n1
```
now **volume group** also created 
to check the status `vgs`

```bash
lvm> vgs
  VG     #PV #LV #SN Attr   VSize  VFree 
  sameer   2   0   0 wz--n- 21.99g 21.99g

```

### Logical Volume

to create use
```bash
#lvcreate -L +size[M,G,K,T] -n lv_name vg_name
# +size M- mb, G- gb, K- kb, T- tb
lvcreate -L +10G -n sameer_lvm sameer
```
to check use `lvs`
after making logical volume then **format into filesystem**
```bash
# mkfs.ext4 /dev/volumegrp/lg_volume
mkfs.ext4 /dev/sameer/sameer_lvm  
```

**mount it**
```bash
mkdir -p /mnt/lv_mount 
#mount [source] [destination]
mount /dev/sameer/sameer_lvm /mnt/lv_mount 
```

### Extend logical volume 
```bash
## lvextend -L size volumegrp_path
lvextend -L +5G /dev/sameer
```
it's take remaining storage from volume group if required we can increase disk size of logical volume size 