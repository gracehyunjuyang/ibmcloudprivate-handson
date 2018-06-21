Mounting additional disk to `var` (IBM Cloud Virtual Server)

## Check disk list using
`dmesg | grep xvd`

## Creating a Primary partition
1. `fdisk -l`
Use `fdisk -l` to show a list of drives and partitions on the system.
1. Determine which disk needs to be set up. Below shows part of the output of running fdisk -l. /dev/xvdb shows one partition, /dev/xvdb1, so /dev/xvdb is not a new disk. /dev/xvdf does not show any partitions under the area whose first column is labelled "Device Boot", so it has not been set up:
```
Disk /dev/xvdb: 2 GiB, 2147483648 bytes, 4194304 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00025cdb

Device     Boot Start     End Sectors Size Id Type
/dev/xvdb1         63 4192964 4192902   2G 82 Linux swap / Solaris


Disk /dev/xvdc: 100 GiB, 107374182400 bytes, 209715200 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/xvda: 100 GiB, 107374182400 bytes, 209715200 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x0b73bd82

Device     Boot  Start       End   Sectors  Size Id Type
/dev/xvda1 *      2048    526335    524288  256M 83 Linux
/dev/xvda2      526336 209715166 209188831 99.8G 83 Linux


Disk /dev/xvdh: 64 MiB, 67125248 bytes, 131104 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000
```

3. `fdisk /dev/xvdc`
1. To create one partition that spans the entire disk, type the letter 'n' and press enter, type the letter 'p' and press enter, type the number '1' and press enter, and then press enter twice to accept the default values for the first and last cylinders. To save and exit, type the letter 'w' and press enter.
1. `fdisk -l` Check if it is mounted.

## Formatting the Partition as ext3 or ext4
1. `mkfs.ext4 /dev/xvdc1`


## Configure `var` folder
1.  Mount the new filesystem under `/mnt`
`mkdir /mnt/var`    
`mount /dev/xvdc1 /mnt/var`

2. Backup data in var only (not the /var directory itself)
`cd /var`
`cp -ax * /mnt/var`

3. Rename the /var directory after your data has been transferred successfully.
`cd /`
`mv var var.old`

4. Make the new var directory
`mkdir var`
5. Unmount the new partition.
`umount /dev/xvdc1`
6. Remount it as /var
`mount /dev/xvdc1 /var`

7. Edit `/etc/fstab` file to include the new partition, with `/var` being the mount point, so that it will be automatically mounted at boot.
`vi /etc/fstab`
`/dev/xvdc1              /var    ext4    defaults                0 0`
8. `reboot`
9. `df -h` Check if it is well mounted. (If `/var` has the specific amount of storage)



#### Referred these links
https://knowledgelayer.softlayer.com/procedure/adding-new-drive-linux
https://unix.stackexchange.com/questions/131311/moving-var-home-to-separate-partition
