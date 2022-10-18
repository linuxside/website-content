---
title: Partition and format memory stick or USB HDD/SSD to exfat filesystem
date: 2022-04-09
updated: 2022-10-18
tags: cli, exfat
url: partition-and-format-memory-stick-to-exfat-filesystem
---

Partition and format any external USB drive (memory stick, HDD, SSD) to MS-DOS exFAT filesystem via CLI.

---

[ExFAT](https://en.wikipedia.org/wiki/ExFAT) partitions have native read/write support across the latest versions of Microsoft Windows OS, macOS and Linux OS.

The OS I chose is **Ubuntu 21**, but it will work in any Debian derived OS, including *Ubuntu*, *Raspbian OS*, *Linux Mint* and so on.

Any of the commands below will run in **command line** (CLI) and they work with desktop and server environments.

1. Install the dependencies

The `exfat-utils` package contains the `mkfs.exfat` and `fsck.exfat` utilities, where the first one creates the exFAT filesystem, while the second one checks and repairs the exFAT filesystem.

If this package is not installed, you can install it by running:

```bash
sudo apt update
sudo apt install exfat-utils
```

2. Find out which drive is the USB drive

```bash
sudo fdisk -l
```

In my case, the device is `/dev/sdd`. **Make sure it's the right device, or you can lose the data on it!**

3. Delete and partition the drive

This step is required only if you want a different partition type or if the drive doesn't have a partition on it.

```bash
sudo fdisk /dev/sdd
```

a. type **d** (delete) as many partitions there are  
b. type **n** (new) and choose primary, then hit enter twice  
c. type **w** (write)  
d. type **q** (quit)  

The standard partition type is Linux (83 in hex). This is not a problem, as the next step will turn our partition into an exFAT.

4. Create an exFAT filesystem:

```bash
sudo mkfs.exfat -n LABEL /dev/sdd1
```

It will output something similar to this:

```text
exfatprogs version : 1.1.0
Creating exFAT filesystem(/dev/sdd1, cluster size=131072)

Writing volume boot record: done
Writing backup volume boot record: done
Fat table creation: done
Allocation bitmap creation: done
Upcase table creation: done
Writing root directory entry: done
Synchronizing...

exFAT format complete!
```

5. Check the newly created filesystem (optional)

**Note:** The partition must be unmounted before running the check command.

```bash
sudo fsck.exfat /dev/sdd1
```

**Resources:**
- [Partitioning with fdisk](https://tldp.org/HOWTO/Partition/fdisk_partitioning.html)
- ['It's FOSS' blog](https://itsfoss.com/format-exfat-linux/)
- [Manpages of exfat-utils in Debian](https://manpages.debian.org/wheezy/exfat-utils/index.html)
- [Labeling an exFAT Partition File System](https://blog.khmersite.net/2021/04/labeling-exfat-partition/)
