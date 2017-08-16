# Misc

Here's the list of the exceptions that can be thrown:

* [Shrink SD Card](#shrink-sd-card)
* [Map Windows Share-folder in Ubuntu](#map-windows-share-folder-in-ubuntu)
* [Links](#links)
* [ESXI Issues](#esxi-issues)
* [InvalidLineNumberException](#invalidlinenumberexception)
* [DifferentLineBreaksFoundException](#differentlinebreaksfoundexception)
* [FileNotFoundException](#filenotfoundexception)
* [IOException](#ioexception)
* [InvalidArgumentException](#invalidargumentexception)

## Shrink SD Card

Firstly, create share folder for Ubuntu VM (/mnt/hgfs/share-folder/).

Then please refer to links:
* [Easy Resize and Back up Raspberry Pi SD Card with Ubuntu](https://www.htpcguides.com/easy-resize-and-back-up-raspberry-pi-sd-card-with-ubuntu/)
* [How to Use SD Card Reader in VMPlayer and VMWorkstation](https://www.htpcguides.com/how-to-use-sd-card-reader-in-vmplayer-and-vmworkstation/)
* [Files missing in /mnt/hgfs on Ubuntu VM?](https://askubuntu.com/questions/591664/files-missing-in-mnt-hgfs-on-ubuntu-vm)

## Map Windows Share-folder in Ubuntu

please refer to link: [How to map a network drive?](https://askubuntu.com/questions/46183/how-to-map-a-network-drive)
* smbclient -L 192.168.2.1 -U jerry
* sudo mount -t cifs -o username=jerry,vers=1.0 //192.168.2.1/jerry /media/share-data/
* if "host is down", use "vers=1.0, or 2.0, 3.0"
* sudo chmod -R 755 /media/share-data
* sudo -i (or su -)

## Links

* [Booting Embedded Linux in One Second](https://embexus.com/2017/05/16/embedded-linux-fast-boot-techniques/)
* [Build a GPS live tracking system](https://embexus.com/2017/07/11/build-a-gps-live-tracking-system/)
* [Diymall Vk-172 G-mouse Usb Gps Dongle u-blox7](http://www.diymalls.com/vk172-GPS-Module)
* google: build embedded linux for diy board
* [Homemade ARM Board Running Linux with LCD](http://www.circuitvalley.com/2015/12/homemade-board-linux-LCD-uboot-porting-corsscompile.html)

## ESXI Issues

* Export/Import(deploy) with `OVF` formats
* Use `BleachBit` to zero free-spaces
* [How to wipe free disk space in Linux?](https://superuser.com/questions/19326/how-to-wipe-free-disk-space-in-linux)
* [Growing, thinning, and shrinking virtual disks for VMware ESX and ESXi](https://kb.vmware.com/s/article/1002019)
* Use `UNetbootin` to write ESXI ISO image (Using `Win32DiskImager` is not working)

## InvalidLineNumberException

```php
<?php

namespace Gnugat\Redaktilo\Exception;

class InvalidLineNumberException extends \InvalidArgumentException implements Exception
{
    public function getLineNumber();
    public function getText();
}
```

## DifferentLineBreaksFoundException

```php
<?php

namespace Gnugat\Redaktilo\Exception;

class DifferentLineBreaksFoundException extends \Exception implements Exception
{
    public function getString();
    public function getNumberLineBreakOther();
    public function getNumberLineBreakWindows();
}
```

## FileNotFoundException

```php
<?php

namespace Gnugat\Redaktilo\Exception;

class FileNotFoundException extends \RuntimeException implements Exception
{
    public function getPath();
}
```

## IOException

```php
<?php

namespace Gnugat\Redaktilo\Exception;

class IOException extends \RuntimeException implements Exception
{
    public function getPath();
}
```

## InvalidArgumentException

```php
<?php

namespace Gnugat\Redaktilo\Exception;

class InvalidArgumentException extends \InvalidArgumentException implements Exception
{
}
```

## Previous readings

* [README](../README.md)
* [Tutorial](01-tutorial.md)
* [Use cases](02-use-cases.md)
* [Reference](03-reference.md)
* [Vocabulary](04-vocabulary.md)
* [Extending](05-extending.md)
