Week 2 Day 4 — Linux Volume Management & AWS EBS

Linux storage can be managed using disks, partitions, and Logical Volume Manager (LVM).
In cloud environments like AWS, storage is usually attached using EBS volumes.

LVM allows flexible disk management such as resizing storage without downtime.

1. Checking Attached Disks

Before creating volumes, check available disks.

Command
lsblk

Example output:

nvme0n1  8G
nvme1n1 10G
nvme2n1 12G
nvme3n1 14G

Meaning:

nvme0n1 → root disk

nvme1n1 → attached EBS

nvme2n1 → attached EBS

nvme3n1 → attached EBS

2. Check Disk Usage
Command
df -h

Shows mounted filesystems and disk usage.

Example:

Filesystem      Size  Used Avail Mounted on
/dev/nvme0n1p1  7G    2G   5G    /

-h means human readable.

3. Mounting a Disk (Without LVM)

First create filesystem.

Format disk
sudo mkfs.ext4 /dev/nvme3n1
Create mount directory
sudo mkdir /mnt/tws_disk_mount
Mount disk
sudo mount /dev/nvme3n1 /mnt/tws_disk_mount
Verify
df -h

You should see the disk mounted.

4. What is LVM?

LVM = Logical Volume Manager.

It allows:

Flexible disk allocation

Combining multiple disks

Resizing storage easily

Better disk management

LVM Components:

Physical Volume (PV)
Volume Group (VG)
Logical Volume (LV)
5. Physical Volume (PV)

Physical Volume represents the actual disk.

Create PV
sudo pvcreate /dev/nvme2n1
View PV
sudo pvdisplay
6. Volume Group (VG)

Volume Group combines multiple physical volumes.

Create VG
sudo vgcreate tws_vg /dev/nvme2n1
View VG
sudo vgdisplay
7. Logical Volume (LV)

Logical volumes are created from volume groups.

Create LV
sudo lvcreate -L 10G -n tws_lv tws_vg

Explanation:

-L → size
-n → name
tws_vg → volume group
View LV
sudo lvdisplay
8. Format Logical Volume

Before using LV, create filesystem.

sudo mkfs.ext4 /dev/tws_vg/tws_lv
9. Mount Logical Volume
Create directory
sudo mkdir /mnt/tws_lv_mount
Mount LV
sudo mount /dev/tws_vg/tws_lv /mnt/tws_lv_mount
Verify mount
df -h

You should see:

/dev/mapper/tws_vg-tws_lv

mounted.

10. Making Mount Permanent

Edit fstab:

sudo nano /etc/fstab

Add entry:

/dev/tws_vg/tws_lv  /mnt/tws_lv_mount  ext4  defaults  0  0

Now it mounts automatically after reboot.

11. Important LVM Commands
List block devices
lsblk
Show disk usage
df -h
Show physical volumes
pvdisplay
Show volume groups
vgdisplay
Show logical volumes
lvdisplay
Remove logical volume
lvremove /dev/tws_vg/tws_lv
Remove volume group
vgremove tws_vg
Remove physical volume
pvremove /dev/nvme2n1
12. DevOps Use Cases

Volume management is used for:

Database storage

Expanding disk space

Managing large servers

Cloud infrastructure scaling

Persistent application storage

What I Practiced

Creating EBS volumes

Attaching disks to EC2

Mounting disks

Creating LVM (PV → VG → LV)

Formatting and mounting volumes

Checking storage with lsblk and df -h

Key Learning

Linux storage management allows flexible and scalable disk management, especially when combined with cloud storage like AWS EBS.
