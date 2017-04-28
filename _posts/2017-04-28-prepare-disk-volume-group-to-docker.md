---
layout: post
published: true
title: Prepare Disk Volume Group to Docker
---


Step 1: First, format the disk. Ex. /dev/xvdb (Yes, I am using Xen) 

```
[root@satelite ~]# fdisk /dev/xvdb 
Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table
Building a new DOS disklabel with disk identifier 0xe02781bc.

Command (m for help): p

Disk /dev/xvdb: 64.4 GB, 64424509440 bytes, 125829120 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0xe02781bc

    Device Boot      Start         End      Blocks   Id  System

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): 
Using default response p
Partition number (1-4, default 1): 
First sector (2048-125829119, default 2048): 
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-125829119, default 125829119): 
Using default value 125829119
Partition 1 of type Linux and of size 60 GiB is set

Command (m for help): p

Disk /dev/xvdb: 64.4 GB, 64424509440 bytes, 125829120 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0xe02781bc

    Device Boot      Start         End      Blocks   Id  System
/dev/xvdb1            2048   125829119    62913536   83  Linux

Command (m for help): t   
Selected partition 1
Hex code (type L to list all codes): 8e
Changed type of partition 'Linux' to 'Linux LVM'

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.

```

Step 2: Create a PV

```
[root@satelite ~]# pvcreate /dev/xvdb1   
  Physical volume "/dev/xvdb1" successfully created.
[root@satelite ~]#
```

Step 3: Create a VG

```
[root@satelite ~]# vgcreate vg-docker /dev/xvdb1
  Volume group "vg-docker" successfully created
[root@satelite ~]#

```

Step 4: Edit the docker configuration to read the VG. You will need the storage-docker-setup script. In Centos 7, it's embedded in docker packages.


```
[root@satelite ~]# cat /etc/sysconfig/docker-storage-setup
# Edit this file to override any configuration options specified in
# /usr/lib/docker-storage-setup/docker-storage-setup.
#
# For more details refer to "man docker-storage-setup"
VG=vg-docker
[root@satelite ~]# 
```

Step 5: Run docker-storage-setup

```
[root@satelite ~]# docker-storage-setup 
  Using default stripesize 64.00 KiB.
  Rounding up size to full physical extent 64.00 MiB
  Logical volume "docker-pool" created.
  Logical volume vg-docker/docker-pool changed.
[root@satelite ~]# 
```

Step 6: Verify your changes

```
[root@satelite ~]# docker info | grep -A 10 'Storage Driver'  
Storage Driver: devicemapper
 Pool Name: vg--docker-docker--pool
 Pool Blocksize: 524.3 kB
 Base Device Size: 10.74 GB
 Backing Filesystem: xfs
 Data file: 
 Metadata file: 
 Data Space Used: 19.92 MB
 Data Space Total: 25.63 GB
 Data Space Available: 25.61 GB
 Metadata Space Used: 53.25 kB
[root@satelite ~]# 

```
