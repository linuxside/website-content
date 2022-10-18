---
title: Disable IPv6
date: 2021-10-17
updated: 2022-04-02
tags: cli, network, ipv6
url: disable-ipv6
---

Method of disabling IPv6 on a system wise level.

---

One of the reason someone would disable IPv6 on his own machine would be the lack of support for it on the remote server. While their DNS advertise AAAA records, their server have IPv6 disabled, making the connections timeout.

I know about the [IPv4 address exhaustion](https://en.wikipedia.org/wiki/IPv4_address_exhaustion), but as long as the system administrators tend to overlook the setup of IPv6 addresses, I will have it disabled on my system.

The OS I chose to do this on is Ubuntu 21, but it will work under a Debian derived distribution and possibly, even on other Linux distributions.

1. edit the sysctl config file

```bash
sudo nano /etc/sysctl.conf
```

2. append at the end of the file

```text
# Disable IPv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
```

3. load the changes to sysctl (without a system reboot)

```bash
sudo sysctl -p
```

**Note:** the changes will remain after a reboot.

**Resources:**
- [archlinux wiki](https://wiki.archlinux.org/title/IPv6#Disable_IPv6)
- [ipv6 test](https://ipv6-test.com/)
- [tuxgraphics blog](http://tuxgraphics.org/npa/disable-ipv6-linux/)
