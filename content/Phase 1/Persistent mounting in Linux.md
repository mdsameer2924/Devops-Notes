[[Disk Management]] 
to persistent mounting disk or partition we use do partition **UUID** entry inside `/etc/fstab` before do it we need to get the partition **UUID**
```bash
sudo blkid /dev/nvme0n1p4 ## enter your parition here 
```
to get   `/dev/nvme0n1p4: UUID="5fcf54fd-4df2-469d-8b04-6d4ea85bec38" BLOCK_SIZE="4096" TYPE="ext4" PARTLABEL="Basic data partition" PARTUUID="fe8f8dfc-05a7-44f1-8130-10f05dfb6037"`

from this output only copy **UUID** and then paste inside `/etc/fstab` like this 
```bash
sudo nano /etc/fstab 
```
as nano editor open inside nano type this 
```nano 
#UUID #mountpoint #filesystem #options #backup #check
UUID=5fcf54fd-4df2-469d-8b04-6d4ea85bec38 /home/sameer/data ext4 defaults 0 2 
```
then `ctrl + X`  then `y` to save the changes

then in terminal reload the systemd to apply the changes
```bash
systemctl daemon-reload
```

to check whether it's work or not just use `sudo mount -a` or 
`lblk` you can show there partition mountpoint exact you given 

### Additional info 
instead of `sudo blkid` we can use 
```bash
lsblk -fs /dev/nvme0n1p4 # to get detials in more details
```
one more things to check that disk or parition usage which mounted in specific dir we did
```bash
df -h /home/sameer/data ## as we add there
```
if it's shows that partition diskusage means successfully work if it's shows root partition disk usage means fstab not work 