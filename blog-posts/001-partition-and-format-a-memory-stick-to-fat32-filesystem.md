---
title: Partition and format a memory stick to FAT32 filesystem
date: 2021-09-02
updated: 2022-10-18
tags: cli, fat32
url: partition-and-format-a-memory-stick-to-fat32-filesystem
---

Partition and format any external USB drive (memory stick, HDD, SSD) to MS-DOS FAT32 filesystem via CLI.

---

Partitioning and formatting an external USB drive to FAT32 filesystem will make it usable in many devices or OS (Linux, Mac, Windows and Android).

The OS I chose is **Debian 10**, but it will work in any Debian derived OS, including *Ubuntu*, *Raspbian OS*, *Linux Mint* and so on.

Any of the commands below will run in **command line** (CLI) and they work with desktop and server environments.

1. Install the dependencies

The `dosfstools` package contains the `mkfs.fat` and `fsck.fat` utilities, where the first one creates the MS-DOS FAT32 filesystem, while the second one checks and repairs the MS-DOS FAT32 filesystem.

If this package is not installed, you can install it by running:

```bash
apt update
apt install dosfstools
```

2. Find out which drive is the USB drive

```bash
fdisk -l
```

In my case, the device is `/dev/sdb`. **Make sure it's the right device, or you can lose the data on it!**

3. Delete and partition the drive

This step is required only if you want a different partition type or if the drive doesn't have a partition on it.

```bash
fdisk /dev/sdb
```

a. type **d** (delete) as many partitions there are  
b. type **n** (new) and choose primary, then hit enter twice  
c. type **w** (write)  
d. type **q** (quit)  

4. Create a FAT32 filesystem

```bash
mkfs.vfat /dev/sdb1
sync
eject /dev/sdb1
```

5. Check the newly created filesystem (optional)

**Note:** The partition must be unmounted before running the check command.

```bash
sudo fsck.fat /dev/sdb1
```

**Resources:**
- [dosfstools Debian homepage](https://tracker.debian.org/pkg/dosfstools)
- [dosfstools GitHub source code](https://github.com/dosfstools/dosfstools)
- [mkfs.fat manual](https://man.archlinux.org/man/mkfs.fat.8)
- [fsck.fat manual](https://man.archlinux.org/man/fsck.fat.8.en)
