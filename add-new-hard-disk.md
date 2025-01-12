#in this example i want add 10TB hard disk 
#to my Linux Server and create a lvm partition 
############################
#Login to server with ssh
lsblk

NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda           8:0    0  100G  0 disk
├─sda1        8:1    0   50G  0 part /
└─sda2        8:2    0   50G  0 part /home
sdb           8:16   0   10T  0 disk

#see sdb  disk is your new disk

#partitioning with parted

parted /dev/sdb
    mklsble gpt
    mkpart primary 0% 100%
    set 1 lvm on
    quit
#create phisical volume
pvcreate /dev/sdb1

#create volume group
vgcreate vg-data1   /dev/sdb1

#create logical volume
lvcreate -L 10TB -n lv-data1 vg-data1

#format the partition
mkfs.ext4   /dev/vg-data1/lv-data1

#mount partition

mkdir /disk1
mount /dev/vg-data1/rl-data1    /disk1

#or you can edit fstab to permanent partitioning
vim /etc/fstab
    /dev/vg-data1/rl-data1  /disk1  ext4    defaults    0 0
#to accept the config
systemctl daemon-reload
mount -a

