---
title: Disable and remove swap
date: 2021-09-24
updated: 2022-10-18
tags: cli, swap
url: disable-and-remove-swap
---

Disable and permanently remove Linux swap

---

There are two types of swap in Linux: **swap partitions** and **swap files**.

The OS I chose to disable swap on is Ubuntu, but I think this will work under any Linux distribution (at least under Debian derived distributions).

1. List the active swaps

```bash
swapon --show
```

This will show you which type of swap you have in your system that will be used in the next step.

An example output:

```text
NAME      TYPE       SIZE USED PRIO
/dev/sdb1 partition 14,9G 3,7M   -2
```

2. Disable swap for current session

If the swap is found on a partition, run:

```bash
sudo swapoff /dev/sdb1
```

Or if the swap is found within a file, run:

```bash
sudo swapoff /swapfile
```

Then

```bash
sudo rm /swapfile
```

**Note:** After you run the command above you must run the 3rd step or your system might fail to boot!

3. Remove swap at boot

The swap info is found in `/etc/fstab` file.

```bash
sudo nano /etc/fstab
```

Search for the line that has swap text in it and comment it out.

**Example:**

```text
UUID=606c8e0e-f961-495b-98a4-1034ad079341 none swap    defaults        0 0
```

becomes

```text
# UUID=606c8e0e-f961-495b-98a4-1034ad079341 none swap    defaults        0 0
```

**Resources:**
- [How to Disable Swap in Linux](https://linuxhandbook.com/disable-swap-linux/)
- [Best way to disable swap in Linux](https://serverfault.com/questions/684771/best-way-to-disable-swap-in-linux)
- [swapoff manual](https://man7.org/linux/man-pages/man8/swapoff.8.html)
