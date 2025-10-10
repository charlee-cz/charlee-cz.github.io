---
title: 'Setting up a Spatial Light Modulator using DLP2000 EVM'
date: 2025-10-10
permalink: /posts/dlp2000
tags:
  - maker
  - DLP
---

This is a blog post for me to document my processes trying to get set-up with

## Background

Following [this paper](https://arxiv.org/pdf/2003.12713)


## Installing TI Drivers

The DLPDLCR2000EVM module is technically deprecated and "out-of-service". The default tutorial links to an older image for the BeagleBone that is not even downloadable anymore. It seems like *bone-debian-9.1-lxqt-armhf-2017-08-31-4gb* might be the last version with the TI drivers installed automatically.

There's various forum posts where people have complained about this, but the "fastest" solution I found was to simply follow the isntructions in [this thread](https://e2e.ti.com/support/dlp-products-group/dlp/f/dlp-products-forum/1559638/dlpdlcr2000evm-i2c-not-detect-on-beaglebone-black). So essentially:

```Bash
sudo echo "uboot_overlay_addr4=/lib/firmware/DLPDLCR2000-00A0.dtbo" >> /boot/uEnv.txt
```

Then confirm that the following line exists in `/boot/uEnv.txt`:

```Bash
# /boot/uEnv.txt 
uboot_overlay_addr4=/lib/firmware/DLPDLCR2000-00A0.dtbo
```

Upon reboot, the driver should be loaded into your BeagleBone Black firmware.


## Example Software

- [An older version of TI support software, including C code to load the buffer](https://github.com/RobertCNelson/boot-scripts/tree/master/device/bone/capes/DLPDLCR2000)
