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

>[! Attention ]+
> Disk label not `appeared` Disk is clean and no partition in disk yet !
> ![[clearndisknoparition.png]]
> 
>
