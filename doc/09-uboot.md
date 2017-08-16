# U-Boot on Beaglebone Black

* [Build U-Boot](#build-u-boot)    
* [Build Kernel](#build-kernel)
* [Create Root Filesystem](#create-root-filesystem)
* [Enable USB Passthrough in ESXI](#enable-usb-passthrough-in-esxi)
* [Create SD Card](#create-sd-card)
* [Access to BBB Serial Console](#access-to-bbb-serial-console)
* [Boot Locally](#boot-locally)
* [Boot Remotely](#boot-remotely)
* [TFTP Rootfs](#tftp-rootfs)
* [Boot over UART](#boot-over-uart)

## Build U-Boot

Consult the following links:
* [Mastering Embedded Linux Programming](https://www.amazon.com/Mastering-Embedded-Linux-Programming-potential/dp/1787283283)
* [Building U-Boot and Linux 3.11 from scratch for the BeagleBone, and booting](https://gist.github.com/eepp/6056325)
* [BeagleBone Black U-Boot](http://www.jumpnowtek.com/beaglebone/Beaglebone-Black-U-Boot-Notes.html)
* [U-Boot on BeagleBone Black](https://www.twam.info/hardware/beaglebone-black/u-boot-on-beaglebone-black)
* [U-Boot on the BeagleBone Black](http://wiki.beyondlogic.org/index.php?title=BeagleBoneBlack_Upgrading_uBoot)

Steps:
* `sudo apt-get install gcc-arm-linux-gnueabihf`
* `sudo apt install device-tree-compiler`
* `wget ftp://ftp.denx.de/pub/u-boot/u-boot-latest.tar.bz2`
* `tar -xjvf u-boot-latest.tar.bz2`
* Edit default SYS_PROMPT in file: /uboot/cmd/Kconfig
* `make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- am335x_boneblack_defconfig`
* `make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j4`
* Install mkimage: `sudo apt install u-boot-tools`


If your strategy should be used instead of another already registered strategy
(ie. they support the same pattern), you can give it a higher priority:

```php
$builder->addSearchStrategy($strategy, 50);
```

> **Important**: The higher the priority is, the sooner the strategy will be
> returned if it supports the given pattern.

> **Note**:A default priority of 0 is assigned to strategies if you don't specify
> it.

## Build Kernel

`Editor` actually uses the `CommandInvoker` in its following methods:

* [Building U-Boot and Linux 3.11 from scratch for the BeagleBone, and booting](https://gist.github.com/eepp/6056325)
* [Compiling the BeagleBone Black Kernel](http://wiki.beyondlogic.org/index.php/BeagleBoneBlack_Building_Kernel)

Steps:
* `git clone -b 4.9 git://github.com/beagleboard/linux.git`
* `make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bb.org_defconfig`
* `make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- -j4`
* `sudo apt-get install lzop`
* `make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- uImage dtbs LOADADDR=0x80008000 -j4`

## Create Root Filesystem

* mkdir bin dev proc sys
* wget http://www.busybox.net/downloads/binaries/1.21.1/busybox-armv7l -O bin/busybox
* chmod +x bin/busybox

## Enable USB Passthrough in ESXI

* Insert USB(SD-card) stick
* Select VM, then `Edit Settings`
* Add `USB Device`, not `USB Controller`
* Start VM

## Create SD Card

* sudo fdisk /dev/sdb: d w
* mkfs.vfat -F16 -v /dev/sdb1
* mkfs.ext4 /dev/sdb2
* mount /dev/sdb1 /mnt/bbone_sd1
* cp /path/to/MLO .
* umount bbone_sd1

## Access to BBB Serial Console

Following link:
* [Two point five ways to access the serial console on your Beaglebone Black](https://dave.cheney.net/2013/09/22/two-point-five-ways-to-access-the-serial-console-on-your-beaglebone-black)

FTDI USB-Serial Converter <=> BBB J1 header:
* J1 pin 2: VSS
* J1 pin 3: RES
* J1 pin 4: TX
* J1 pin 5: RX

Connect to BBB:
* check tty assignment: dmesg
* sudo screen /dev/ttyUSB0 115200,cs8

## Boot Locally

* setenv bootargs "earlyprintk console=ttyO0,115200n8 root=/dev/mmcblk0p2 rootwait ro rootfstype=ext4 init=/bin/init"

## Boot Remotely
* setenv serverip 192.168.2.139
* setenv ipaddr 192.168.2.193
* tftpboot 0x80200000 zImage
* tftpboot 0x80f00000 am335x-boneblack.dtb
* setenv npath /home/jerry/rootfs
* setenv bootargs console=ttyO0,115200 root=/dev/nfs rw nfsroot=${serverip}:${npath} ip=${ipaddr}
* bootz 0x80200000 - 0x80f00000

After login:
* mount -t proc proc /proc
* fdisk -l
* mount
* mount /dev/mmcblk0p2 /mnt
* cp -a /home/myrfs/* .
* umount mnt

Reboot:
* setenv bootargs "earlyprintk console=ttyO0,115200n8 root=/dev/mmcblk0p2 rootwait rw rootfstype=ext4"

## TFTP Rootfs

Refer to [Writing to SD partitions from u-boot](https://lists.denx.de/pipermail/u-boot/2014-February/174589.html)
* tftpboot 0x80200000 core-image-sato-beaglebone.ext4
* mmc part
* mmc write 0x80200000 0x20800 0x639D8

## Boot over UART

Use TeraTerm terminal. Please refer to [AM335x U-Boot User's Guide](http://processors.wiki.ti.com/index.php/AM335x_U-Boot_User%27s_Guide)

## Next readings

* [Exceptions](06-exceptions.md)

## Previous readings

* [README](../README.md)
* [Tutorial](01-tutorial.md)
* [Use cases](02-use-cases.md)
* [Reference](03-reference.md)
* [Vocabulary](04-vocabulary.md)
