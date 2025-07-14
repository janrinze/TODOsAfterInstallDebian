# TODOs after installing Debian testing/bookworm on Aarch64

In general LXQT or LXDE is a good alternative for lightweight desktops.

## Libre Office under LXQT is extremely slow
### solution:
Add `SAL_USE_VCLPLUGIN=qt5` to `/usr/share/lxqt/session.conf` under the category `[Environment]`

## Default utillities are missing
```
apt install net-tools apt-file
```

## Unnecessary packages that eat lots of CPU
```
apt remove --purge ofono connman
```

Because connman handles networking we need to have in /etc/network/interfaces :
```
# interfaces(5) file used by ifup(8) and ifdown(8)
# Include files from /etc/network/interfaces.d:
source /etc/network/interfaces.d/*

allow-hotplug eth0
iface eth0 inet dhcp

# allow-hotplug wlan0
iface wlan0 inet dhcp
        wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

```

## Plank has sometimes trouble starting

add a file `/usr/bin/startplank` :
```
#! /bin/bash

if [[ ! -z "$1" ]]
then
    sleep $1
fi

plank >/dev/null 2>&1 &

```

replace the command in the session settings to use `startplank 2` instead of `plank`.

## Fonts too small on 4K monitor
add a file `.Xresources` to your home directory containing:
```
Xft.dpi: 192

! These might also be useful depending on your monitor and personal preference:
Xft.autohint: 0
Xft.lcdfilter:  lcddefault
Xft.hintstyle:  hintfull
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

```

## Disable side search in chrome
https://www.reddit.com/r/chrome/comments/15hgvim/comment/jvssn5d/
```
enigmamonkey
28 days ago
Now you have to trigger 3 goddamned flags. It's just getting shittier and shittier.

Side search

Search web in side panel

And now: CSC
```

## Function keys on MBpro

```
echo options hid_apple fnmode=2 | sudo tee -a /etc/modprobe.d/hid_apple.conf
sudo update-initramfs -u -k all
```
Will be active after reboot.
