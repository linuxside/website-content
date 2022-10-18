---
title: Installing IceWM on Debian netinstall
date: 2021-10-11
updated: 2022-04-02
tags: cli, icewm
url: installing-icewm-on-debian-netinstall
---

Set up a small footprint (memory and storage) GUI solution.

---

This tutorial will help you set up a small footprint (memory and storage) basic GUI solution.

The OS I chose to do this on is Debian 11.

1. Login as root

```bash
su
```

2. Install IceWM

```bash
apt update
apt install icewm xinit alsa-utils
```

**Note:** `alsa-utils` is optional, but without it, you will have no sound.

3. Logout from root

```bash
exit
```

4. Autostart IceWM after non-root user login

```bash
nano ~/.bashrc
```

and paste:

```bash
if [[ -z $DISPLAY ]] && [[ "$(tty)" = "/dev/tty1" ]]; then
  exec startx
fi
```

5. Reboot to see it in action

```bash
systemctl reboot
```

**Resources:**
- [The difference between a desktop environment and a window manager](https://askubuntu.com/questions/18078/what-is-the-difference-between-a-desktop-environment-and-a-window-manager)
- [IceWM - ArchWiki](https://wiki.archlinux.org/title/IceWM)
- [Using IceWM and a Raspberry Pi as my main PC](https://raymii.org/s/blog/Using_IceWM_and_sharing_my_config_and_tips_tricks.html)
