before create partition here are some prerequisites

### Requirements
- Having `Sudo` privileged  user account 
- enough disk space already in disk not full 
- Partition tool installed in Linux system  like [[fdisk]] , [[parted]]

then, need to [[Understand Partition Table]], 

**Check partition type**
```bash
sudo fdisk -l # search for Disklabel type: either gpt or dos
```

![[disklabel type.png]]
after this command go to each label and check `gpt` or `dos`, 
**dos** refers to MBR partitions tables used 

> [!Attention]+
> Disk label not `appeared` Disk is clean and no partition in disk yet !  
>  ![[clearndisknoparition.png]]


### Identify target disk or partition
before do any partition select correct disk or partition,
wrong disk might be data lost,

#### fdisk -l or lsblk 
we can check the disk list of partitions using these two command 
**lsblk** provide clean tree format of disk unlike **fdisk** which provide verbose detailed 
disk listing 

```bash
lsblk #list disk blocks
```
![[lsblk block list.png]]

as we show our disk is `nvme0n1` means it's disk 1 
if there would be other disk it's shows `nvme0n2` as well 
**Conceptual Understanding**
- my disk shows `sda` 
- some system might be shows `nvme0n1` or `sda` 
it's depend  system use `hdd` or `sata ssd`
- **sata ssd /hhd :** sda 
- **nvme ssd :** nvme0nx , where x is disk number 

now i've choose `sda` 
choose disk what you target 


> [!tip] keep in mind
> remember either disk is empty or 
   have proper backup


### Creating Partition 
**disk i choose  :**  `sda`
**Tool used   :** `fdisk`

for creating partition give command 
```bash
fdisk /dev/sda #replace sda with your target
```

![[fdisk devsda.png]]

in my system there is no such partition table hence for creating partition table 
you have choice press `g` for **GPT** and press `o` for `dos` **MBR** ,
> i choose g to create my partition table

now after this press `n` to **create new partition** then it's ask for 
```bash
Command (m for help): n
Partition number (2-128, default 2): #press enter
First sector (73402368-88583646, default 73402368): #press enter 
Last sector, +/-sectors or +/-size{K,M,G,T,P} (73402368-88583646, default 88582143): +35G  #press enter 
```

```bash
Created a new partition 1 of type 'Linux filesystem' and of size 35 GiB.

```

in your `Last sector` gives your partition size use **`+nG`** where **n =** number and **G =** gib
**M** = mib, **T =** tib etc 

**Check partition status**
press `p` to check:

```bash
Command (m for help): p

Disk /dev/sda: 42.24 GiB, 45354844160 bytes, 88583680 sectors
Disk model: VBOX HARDDISK   
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 912BCC81-BC5C-4448-B789-2A17787FA8F9

Device     Start      End  Sectors  Size Type
/dev/sda1   2048 73402367 73400320   35G Linux filesystem

```

shows similar if your choose `GPT` . 

when your are satisfy press `w` to permanent safe remember there is no return back if you press `w` and press `q` to quit without saving

**final result**
![[Pasted image 20260702185300.png]]

### Partition Formatting
before formatting you can know more about [[file system format]]

partition formatting into file system crucial to make partition able to stored data.
use `mkfs` command to **make file system**, two popular choice of filesystem in linux 
[[ext4]] and [[xfs]]

```bash
mkfs.ext4 /dev/sda1 #make sure correct partition
```
> to do this data lost inevitable make sure untouched partition or target partition formatting you do.


[[Persistent mounting in Linux]]
[[Arch linux partition]]