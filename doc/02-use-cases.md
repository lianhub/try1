# IgH EtherCAT Master

This page instructs how to set up IgH EtherCAT master on raspberry PI-3.

Please follow the steps below:

* [Setup RT-Preempt](#setup-rt-preempt)
 * [Download](#download)
 * [Patch](#patch)
 * [Prevent freezing](#prevent-freezing)
* [Build EtherCAT](#build-ethercat)
 * [Configuration](#configuration)
 * [Copy](#copy)
* [Install Machinekit](#install-machinekit)
* [Install Linuxcnc-Ethercat](#install-linuxcnc-ethercat)
* [Beaglebone Issue](#beaglebone-issue)
* [Yocto-SDK Issue](#yocto-sdk-issue)
* [Previous readings](#previous-readings)

## Setup RT-Preempt

Many projects use the YAML format in their configuration files.

### Download

* Release date: 2017-08-16
* Kernel version: 4.9
* uname-a: Linux raspberrypi 4.9.41-v7+ #1023 SMP Tue Aug 8 16:00:15 BST 2017 armv7l GNU/Linux
* uname-a: Linux raspberrypi 4.9.43-rt30-v7+ #1 SMP PREEMPT RT Thu Aug 17 12:23:30 EDT 2017 armv7l GNU/Linux

### Patch

Follow these instructions in file "Machinekit-RT-Preempt-RPI.md" at: [Get a basic Machinekit / EtherCAT system on the Raspberry PI 3 Model B](https://github.com/koppi/mk)

* Patch: patch-4.9.40-rt30.patch.gz

> **Note**: see `BundleRoutingTest` for an actual implementation.

### Prevent freezing

Follow these instructions modify /boot/cmdline.txt: [Freezing with RT-patch (Pi 3)](https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=159170)

* Add this: `dwc_otg.fiq_fsm_enable=0 dwc_otg.fiq_enable=0 dwc_otg.nak_holdoff=0`

It appears that what did the trick has been the order of the fiq disable commands. dwc_otg.fiq_fsm_enable=0 must be set *before* dwc_otg.fiq_enable=0. The other way around it finds fiq_fsm_enable true with fiq_enable false, and it forces fiq_enable true.

## Build EtherCAT

* sudo apt install autoconf libtool
* ./configure --enable-generic --disable-8139too

> **Note**: be sure that you keep the /opt/linux folder: --with-linux-dir.

### Configuration

Copy folder to: etc/sysconfig/, and edit file `ethercat`:
* sudo cp -r /opt/etherlab/etc/sysconfig /etc/
* MAC address,
* "generic",
* run "depmod" (after make modules_install), not modprobe!

## Install Machinekit

Install packages: machinekit, machinekit-dev, machinekit-rt-preempt!
* sudo dpkg -i *.deb
* sudo apt install gdebi
* sudo apt --fix-broken install
* dpkg-repack

## Install Linuxcnc-Ethercat

Copy to appropriate folders: lcec.so, lcec_conf, libethercat.so
* make
* sudo make install
* /usr/bin/lcec_conf
* sudo cp /usr/lib/linuxcnc/posix/lcec.so /usr/lib/linuxcnc/rt-preempt/lcec.so
* sudo cp /opt/etherlab/include/ecrt.h /usr/include/linuxcnc/
* sudo cp /opt/etherlab/lib/libethercat.so.1 /usr/lib/linuxcnc/rt-preempt/
* sudo cp /opt/etherlab/lib/libethercat.so /usr/lib/linuxcnc/rt-preempt/

To run machinekit:
* machinekit /usr/share/linuxcnc-ethercat/examples/.../*.ini
* machinekit test.ini

## Beaglebone Issue

As stated in video [Machinekit + EtherCAT on BeagleBone Black ](https://www.youtube.com/watch?v=M1LxQBjttWg):

> **Note**: The external NIC is used due to the need of preservation of the on board NIC
> for LAN operation and the fact that the SoC has an integrated switch, wich affected real
> time capability.

An interesting article is [Using the Beaglebone PRU to achieve realtime at low cost](https://www.embeddedrelated.com/showarticle/586.php)

## Yocto-SDK Issue

* Refer to [populate_sdk and kernel headers](https://lists.yoctoproject.org/pipermail/yocto/2015-July/025475.html)
* add: IMAGE_INSTALL_append=" kernel-devsrc"
* or use: core-image-sato-sdk
* sudo chown -R jerry:jerry folder
* chmod +x ./-libtool
* [libtoolize -f before ./configure](https://github.com/Achillefs/geoip/issues/3)
* [./configure --disable-dependency-tracking](https://github.com/joakim666/colortail/issues/14)
* ./configure --with-linux-dir=$sysroots/usr/src/kernel/
* make scripts (/usr/src/kernel/), refer to [linux/scripts/recordmcount: No such file or directory](https://stackoverflow.com/questions/13766383/linux-scripts-recordmcount-no-such-file-or-directory)

## Previous readings

* [README](../README.md)
* [Tutorial](01-tutorial.md)
