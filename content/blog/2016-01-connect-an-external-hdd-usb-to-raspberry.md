---
title: "CONNECT AN EXTERNAL HDD (USB) TO RASPBERRY PI"
slug: "connect-an-external-hdd-usb-to-raspberry"
date: "2016-01-06"
tags:
  - "hdd usb"
  - "raspberry pi"
authors: [Guillermo Guerrero]
banner: "media/raspberry-pi.png"
aliases:
  - "/blog/connect-an-external-hdd-(usb)-to-raspberry"
---

In `Raspberry Pi B` model by default is limiting the output amperage. We can trick this behavior editing the config file:

```
vi /boot/config.txt
```

Add the following lines:

```
safe_mode_gpio=4
max_usb_current=1   
```

Reboot the raspberry and now you can plug the HDD in the usb port.
