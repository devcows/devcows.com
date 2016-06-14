---
title: "Be sync with Raspberry Pi"
slug: "be-in-sync-with-raspberry"
date: "2016-01-06"
tags:
  - "mikrotik"
  - "vpn"
  - "ipsec"
author: "GUILLERMO"
image: "media/BTSync.png"
---

Is very common have the necessity to sync some kind of information with other computers or have a synchronize backup. In this post we explain how to install [Btsync](https://getsync.com) into the Raspberry PI.

## Download

```
mkdir .btsync
cd .btsync
wget https://download-cdn.getsyncapp.com/stable/linux-arm/BitTorrent-Sync_arm.tar.gz
tar -xvf BitTorrent-Sync_arm.tar.gz
rm BitTorrent-Sync_arm.tar.gz

ln -s /lib/arm-linux-gnueabihf/ld-linux.so.3 /lib/ld-linux.so.3
```

## Configure

```
cd ~/.btsync
./btsync --dump-sample-config > btsync.conf
# browse the sample config file and change what you want
```

## Start at boot

```
nano /etc/init.d/btsync
```

Paste the following code in the script:

```
#! /bin/sh
# /etc/init.d/btsync
#

# Carry out specific functions when asked to by the system
case "$1" in
start)
    /home/osmc/.btsync/btsync --config /home/osmc/.btsync/btsync.conf
    ;;
stop)
    killall btsync
    ;;
*)
    echo "Usage: /etc/init.d/btsync {start|stop}"
    exit 1
    ;;
esac

exit 0
```

Then change the permissions, test, and register it to run at boot:
```
sudo chmod 755 /etc/init.d/btsync
sudo /etc/init.d/btsync start       # test that the script starts
sudo /etc/init.d/btsync stop        # test that the script stops
sudo update-rc.d btsync defaults
```
