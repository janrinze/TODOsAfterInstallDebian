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
