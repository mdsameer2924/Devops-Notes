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
![[Pasted image 20260702174726.png]]

as we show our disk is `nvme0n1` means it's disk 1 
if there would be other disk it's shows `nvme0n2` as well 
**Conceptual Understanding**
- my disk shows `sda` 
- some system might be shows `nvme0n1` or `sdb` 
it's depend  system use `hdd` or `sata ssd`
- **sata ssd & hhd :** sda 
- **nvme ssd :** nvme0nx , where x is disk number 


