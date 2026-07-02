Partition table is used to make the partition persistent and the table entry do in 
`/etc/fstab`   

`fstab` contains all partition records to permanent mount 
without `fstab` partition mount only temporary.

## Types of Partition Table 
1. **MBR** - Master Boot record
2. **GPT** - guid Partition Table

### MBR
this parition is used for legacy system or older hardware  and address limit upto **`2.2`TB** 
becuase of it's 32bit and 
it's  `2³² -1` =  4.3 billiom approx 
`512 byte sector X 4.3billion = 2.199TB`